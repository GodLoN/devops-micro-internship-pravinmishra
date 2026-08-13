# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

![Screenshot 1](screenshots/week-5-assign-5-task-1-ss-1.png)

### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

Jira Cloud's REST API authenticates requests using Basic Authentication over HTTPS, which strictly requires combining the user's Atlassian account email address (the username) and the secret API token (the password). The API token proves identity, while the account email specifies which user profile holds the authorization permissions. Additionally, because Atlassian hosts thousands of distinct tenant instances, the Jira site URL is required to tell the MCP server which exact Jira instance and network endpoint to route the API calls to.

---

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

![Screenshot 2](screenshots/week-5-assign-5-task-2-ss-2.png)

### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

Despite the runtime difference (npx for Node.js vs uvx for Python), the exact JSON structure remains identical: both define a "command", an array of "args", and an "env" object. Claude Code does not care which programming language an MCP server is written in because MCP uses a standardized protocol abstraction layer communicating over standard input/output (stdin/stdout) via JSON-RPC. As long as the process initiated by the command speaks valid MCP JSON-RPC messages, Claude Code can interact with the server's tools seamlessly regardless of the underlying programming language.

---

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

![Screenshot 3](screenshots/week-5-assign-5-task-3-ss-3.png)

### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

The .mcp.json file defines server configurations and is intended to be committed to version control (such as GitHub) so the entire development team shares the same MCP setup. In contrast, JIRA_API_TOKEN is a sensitive security credential that grants access to your Atlassian account. Placing secrets in .mcp.json creates a critical risk of exposing credentials publicly or across repositories. By storing sensitive environment variables in settings.local.json and listing that file in .gitignore, credentials remain local to your machine while allowing safe repository collaboration.

---

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

![Screenshot 4](screenshots/week-5-assign-5-task-4-ss-4.png)

---

# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

![Screenshot 5](screenshots/week-5-assign-5-task-5-ss-5.png)

### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

I confirmed this was real board data using the following verification steps:

1. Live MCP Server Query: The data was pulled directly from the Jira API via the Jira Model Context Protocol (mcp-atlassian / jira) integration rather than relying on standard AI text generation.

2. Specific Entity Keys: The report references verified Jira issue keys (DMIWGO-16, DMIWGO-3, and DMIWGO-2) that match the specific project workspace (DMI-SPRINT-HEALTH).

3. Exact Sprint Metadata: The active sprint parameters (Sprint 1 timeframe: August 8, 2026 – August 22, 2026, active status, story point distribution, and exact assignee name) reflect live state values fetched directly from the Jira board endpoint.


---

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

![Screenshot 6](screenshots/week-5-assign-5-task-6-ss-6.png)

#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

![Screenshot 7](screenshots/week-5-assign-5-task-6-ss-7.png)

### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

* **Included Tools:** The skill's allowed-tools list exclusively includes read-only Jira tools such as jira_get_all_sprints, jira_get_sprint_issues, jira_search_issues, jira_get_issue, and jira_get_project_details (along with the file system Read tool).

* **Excluded Mutating Tools:** It deliberately excludes all state-changing or mutating tools, specifically jira_create_issue, jira_update_issue, jira_transition_issue, and jira_add_comment (as well as file system Write or Edit tools).

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

* **Maintaining Role Boundaries & Team Trust:** A Scrum Master acts as a servant leader and facilitator whose primary responsibility is observing, reporting, and clearing blockers for the team—not modifying the backlog or forcing task states unilaterally.

* **Preventing Unintended Board Alterations:** Restricting the /sprint-health tool to read-only guarantees that automated health checks and sprint audits cannot accidentally alter issue statuses, reassign tickets, or modify story points during live sprint monitoring.

---

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

![Screenshot 8](screenshots/week-5-assign-5-task-7-ss-8.png)

### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

* **Accountability and Governance:** AI models can assess sprint risk and identify state changes through read-only tools, but actual state changes (such as closing a ticket, reassigning tasks, or altering story points) directly impact team accountability, velocity tracking, and project delivery deadlines.

* **Context and Intent Validation:** A Scrum Master or engineer possesses real-world context—such as unblocked dependencies, verified code merges, or manual QA sign-offs—that an automated LLM skill cannot observe from board metadata alone. Keeping execution in human hands prevents accidental, invalid, or premature ticket transitions while maintaining human oversight over board integrity.

---

# Submission Instructions

Complete all tasks in sequence.

Your submission must include:
- All 8 required screenshots
- All the required notes

---

# Completion Checklist

- [ ] Task 1: Jira API token created, value never screenshotted (Screenshot 1)
- [ ] Task 2: `.mcp.json` has the Jira server block (Screenshot 2)
- [ ] Task 3: Credentials stored in `settings.local.json`, token blurred, file gitignored (Screenshot 3)
- [ ] Task 4: `/mcp` shows the Jira server connected (Screenshot 4)
- [ ] Task 5: Live query returned real sprint data, verified against the browser (Screenshot 5)
- [ ] Task 6: `/sprint-health` skill created with correct read-only `allowed-tools`, and produced a full report (Screenshots 6–7)
- [ ] Task 7: A manual board change was reflected in a second `/sprint-health` run (Screenshot 8)
- [ ] Skill never created, edited, transitioned, or commented on any issue
- [ ] Reflection answered (Notes)
- [ ] No API token value exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
