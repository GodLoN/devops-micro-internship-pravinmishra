# Assignment 4 — Building Your AI Team

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build and configure a set of specialized AI subagents inside your project. You will learn how different models and tool permissions define agent behavior, and you will trigger two real agent delegations to analyze security and cost aspects of your Terraform infrastructure.

---

# Task 1 — Create the Agents Folder and Add Files

## Goal

Create the `.claude/agents/` directory and add all required agent files.

### Evidence

#### Screenshot 1 — Agents folder structure in VS Code

![Screenshot 1](screenshots/assign-1-task-1-ss-1.png)

---

# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?

Cost optimization checks do not require deep architectural or policy reasoning; they only need to scan resources, match patterns, and compare baseline settings like pricing classes and storage tiers. Using Claude Haiku handles these simple checks perfectly while maximizing execution speed and stopping you from overpaying for expensive compute.

---

#### 2. Why does the security auditor NOT have Write in its tools list?

Following the principle of least privilege, a security audit should only inspect infrastructure, never modify it. Restricting the security auditor to read-only tools (read, grep, glob) eliminates the risk of an AI worker accidentally altering or introducing bugs into your live codebase during a routine review.

---

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

Code generation quality heavily depends on the reasoning depth of the underlying model, meaning complex infrastructure updates require maximum intelligence. Setting the model to inherit provides the flexibility for the sub-agent to automatically scale up to the level of whatever model (such as Claude Opus or Sonnet) you are currently running in your main active session.

---

### Evidence

#### Screenshot 2 — security-auditor.md frontmatter

![Screenshot 2](screenshots/assign-4-task-2-ss-2.png)

---

#### Screenshot 3 — cost-optimizer.md frontmatter

![Screenshot 3](screenshots/assign-4-task-2-ss-3.png)
---

# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — Security auditor delegation triggered

![Screenshot 4](screenshots/assign-4-task-3-ss-4.png)

---

#### Screenshot 5 — Security audit report output

![Screenshot 5](screenshots/assign-4-task-3-ss-5.png)

---

# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — Cost optimization report output

![Screenshot 6](screenshots/assign-4-task-4-ss-6.png)

---

# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your Google Doc submission
- Push final changes to your forked GitHub repository
- Submit only the Google Doc link as required

---

## Google Doc Link

Paste your Google Doc URL here:

'https://docs.google.com/document/d/1R3rBXrucIv_pnvvul-7YZEqA9wc0BfvM6jzU16ubHIc/edit?usp=sharing'

---

## GitHub Repository URL

Paste your forked repository URL here:

'https://github.com/GodLoN/Ultimate-Agentic-DevOps-with-Claude-Code.git'

---

# Completion Checklist

- [ ] `.claude/agents/` folder contains all 3 agent files
- [ ] Screenshot 2 shows correct `security-auditor.md` configuration
- [ ] Screenshot 3 shows correct `cost-optimizer.md` configuration
- [ ] All 3 written answers completed in Google Doc
- [ ] Security auditor executed successfully
- [ ] Cost optimizer executed successfully
- [ ] Security report is visible with findings
- [ ] Cost report is visible with recommendations
- [ ] All required screenshots added
- [ ] GitHub repo updated with agents

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