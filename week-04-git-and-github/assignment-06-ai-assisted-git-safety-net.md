# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

Add your screenshot here.

---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

Add your answer here.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

![Screenshot 1](screenshots/week-4-assign-6-task-1-ss-1.png)

---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

Committing real credentials to Git history—even briefly or on private branches—exposes them to severe security risks, automated scraping, and immediate credential compromise. Using an obviously fake key (such as AKIAABCDEFGHIJKLMNOP) safely simulates a secret detection pattern during local testing without risking leakages, account takeovers, or cloud infrastructure compromise.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

![Screenshot 2](screenshots/week-4-assign-6-task-2-ss-2.png)

---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

![Screenshot 3](screenshots/week-4-assign-6-task-2-ss-3.png)

---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Files inside the local .git/ folder are ignored by version control and cannot be pushed to remote repositories. By tracking hooks/pre-commit directly in the repository directory and referencing it via git config core.hooksPath hooks, the pre-commit checks become part of the codebase. This ensures that every team member who clones the repository automatically inherits and enforces the exact same security gates and quality standards.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

* PreToolUse intercepts agentic AI actions before an AI tool executes a potentially dangerous shell command or file edit.

* Git Pre-Commit Hook intercepts local developer actions right before Git creates a commit snapshot in version control.

* Commonality: Both serve as deterministic "safety rails" (gatekeepers) that evaluate input parameters against predefined security rules and abort the operation prior to execution if a policy violation occurs.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

![Screenshot 4](screenshots/week-4-assign-6-task-3-ss-4.png)

---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line that matched was:
if git diff --cached -- "$file" | grep -qE 'AKIA[0-9A-Z]{16}|-----BEGIN (RSA|OPENSSH|PRIVATE) KEY-----'; then
It matched because the regex pattern AKIA[0-9A-Z]{16} specifically looks for the standard 20-character AWS Access Key structure starting with the prefix AKIA followed by 16 uppercase alphanumeric characters.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

No, it would not have caught it unless the secret matched an exact hardcoded regex pattern in the script. This highlights the fundamental limitation of fixed-rule pattern matching: deterministic rules are rigid and can only catch known patterns. They miss obfuscated credentials, custom secret naming conventions, or context-specific risks that fall outside their exact regex definitions.
---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

![Screenshot 6](screenshots/week-4-assign-6-task-4-ss-5.png)

---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

![Screenshot 6](screenshots/week-4-assign-6-task-4-ss-6.png)

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

The /pr-ready skill is designed strictly for inspection, risk analysis, and drafting documentation. Excluding the Write tool guarantees that the AI remains read-only, preventing it from silently modifying code files, staging unauthorized changes, or bypassing human oversight during pre-PR evaluation.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

* **Pre-Commit Hook (Fixed Rule):** Flagged the AKIA key pattern because it matched its hardcoded regex, but it ignored the left*over echo "DEBUG: ..." statement because no rule was written to block echo.

* **/pr-ready Skill (AI Review):** Flagged both the credential-shaped string and the leftover DEBUG print statement. The AI recognized the contextual noise of leftover debug code, demonstrating how semantic AI evaluation catches qualitative code quality issues that rigid rules miss.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

![Screenshot 7](screenshots/week-4-assign-6-task-5-ss-7.png)

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

![Screenshot 8](screenshots/week-4-assign-6-task-5-ss-8.png)

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I edited scripts/notify.sh to remove the hardcoded credential variable (AWS_ACCESS_KEY_ID=AKIAABCDEFGHIJKLMNOP) and deleted the leftover echo "DEBUG..." statement. After saving and re-staging the clean file (git add scripts/notify.sh), the staged diff no longer contained any patterns matching the hook's regex, allowing git commit to execute cleanly.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

![Screenshot 9](screenshots/week-4-assign-6-task-6-ss-9.png)

---

#### PR Link

'https://github.com/GodLoN/devops-micro-internship-pravinmishra/pull/1'

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I did not edit the draft provided by /pr-ready and used it word-for-word. The draft generated by the skill (docs: Complete week 04 git and GitHub assignments...) already accurately summarized the scope of my changes, covered the exact completion steps, and provided a clear explanation without hallucinating unperformed tasks or missing key context.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

If an AI draft contains inaccuracies or hallucinations and is blindly copy-pasted, it can mislead reviewers about what actually changed in the diff, claim that tests or features were added when they weren't, or obscure critical breaking changes. In a real engineering team, this creates confusion during code reviews and pollutes the repository's audit history.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This PR includes local practice scripts (scripts/notify.sh), pre-commit hooks, and custom AI skills (.claude/skills/pr-ready/SKILL.md) specific to this assignment. Targetting the shared upstream repository (pravinmishraaws) with these personal training artifacts would pollute the central repository with non-upstream code, whereas targeting my own fork keeps my practice work isolated and cleanly documented.
---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

* Running git diff --cached, git status, and checking file sizes via git cat-file to extract the staged metadata.

---

**2. Which step(s) represent Analyze?**

* The pre-commit hook scanning staged text against regex/size rules, and the /pr-ready skill evaluating code context, searching for debug logs, and drafting the PR report.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

The Human Act step occurs when the engineer manually executes git commit, git push, and clicks "Create Pull Request". A human must run these because critical state changes in a shared codebase require human accountability, verification, and decision-making—AI should advise, but never take write/deploy actions autonomously.

---

**4. Which step is Verify?**

Running the pre-commit hook again upon committing, re-running /pr-ready to confirm a clean risk report, and reviewing the target branch on GitHub before submitting.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

You need both because fixed-rule hooks provide fast, non-negotiable security gates for known risks (like hardcoded keys or large files), while AI skills provide contextual judgment for qualitative issues (like debug clutter or poor PR descriptions). Together, deterministic rules handle security while AI enhances code quality and human context.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

'https://www.linkedin.com/posts/godwin-obi-008a12177_dmibypravinmishra-git-github-share-7486207670488662017-_TLL/?utm_source=share&utm_medium=member_desktop&rcm=ACoAACn5hogBVyHnSR92cyBf5EzFBZEMSepEVPM'

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

* **Dual-Layer Git Security:** Learned how to combine fast, deterministic rules (Bash pre-commit hooks) for non-negotiable security gates with Agentic AI skills (/pr-ready) for qualitative, contextual code reviews.

* **Tracked Repository Hooks:** Discovered how to move local Git hooks out of .git/hooks/ and track them in the main repository directory using git config core.hooksPath hooks, ensuring automated security gates are enforced across the entire team.

* **Principle of Least Privilege for AI:** Built a restricted Claude Code skill configured with allowed-tools: Bash, Read, Grep (excluding Write), proving that AI assistants should be given read-only access when performing inspection and drafting tasks.

* **Deterministic Rules vs. Contextual AI:** Experienced firsthand why regex pattern matching catches explicit secrets (AKIA...) in milliseconds, while AI review excels at detecting soft issues like leftover debug statements (echo "DEBUG..."), missing documentation, or scope creep.

* **The Agentic Loop in Practice:** Mastered the Gather → Analyze → Human Act → Verify pattern, reinforcing that AI should gather facts and draft recommendations, but human engineers must always review, approve, and execute critical Git state changes (commit, push, and PR creation).

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

`https://github.com/GodLoN/devops-micro-internship-pravinmishra.git`

---

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

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
