# Capstone Assignment — Deploy the Book Review App Using Terraform and Claude Code Agentic AI

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Student Details

**Full Name:** Godwin Obi
**Cloud Platform:** AWS  
**GitHub Repository URL:** https://github.com/GodLoN/book-review-app.git 
**Public Application URL / Load-Balancer DNS:** http://book-review-dev-public-alb-867081177.us-east-2.elb.amazonaws.com

---

## Purpose

Deploy the Book Review App using Terraform on AWS or Azure in a secure, highly available, production-style three-tier architecture. Use Claude Code, specialized subagents, Terraform MCP, and validation hooks to support the engineering workflow while keeping all infrastructure-changing operations under human control.

---

# Task 0 — Prepare the Project and Agentic AI Environment

## Goal

Prepare the Book Review App project and configure the provided Claude Code Agentic AI starter kit with project context, specialized subagents, Terraform MCP, validation hooks, and safety guardrails.

## Evidence

### Screenshot 1 — Project `CLAUDE.md`

Add a screenshot of the project `CLAUDE.md` showing the three-tier architecture, security boundaries, Terraform requirements, and human-approval rules.

![Screenshot 1](screenshots/week-8-assign-5-task-0-ss-1.png)

---

### Screenshot 2 — Terraform Engineer Subagent

Add a screenshot showing the Terraform Engineer subagent configuration.

![Screenshot 2](screenshots/week-8-assign-5-task-0-ss-2.png)

---

### Screenshot 3 — Architecture and Security Reviewer Subagent

Add a screenshot showing the Architecture and Security Reviewer subagent configuration.

![Screenshot 3](screenshots/week-8-assign-5-task-0-ss-3.png)

---

### Screenshot 4 — Terraform MCP Connection

Add a screenshot showing Terraform MCP connected and available.

![Screenshot 4](screenshots/week-8-assign-5-task-0-ss-4.png)

---

### Screenshot 5 — Validation Hooks

Add a screenshot showing the configured Claude Code validation hooks.

![Screenshot 5](screenshots/week-8-assign-5-task-0-ss-5.png)

---

# Task 1 — Design the Three-Tier Architecture

## Goal

Design the required secure, highly available three-tier architecture and create an architecture diagram before building the infrastructure.

The diagram must show:

- VPC or VNet
- Availability Zones or equivalent availability locations
- Six subnets
- Internet connectivity
- NAT or outbound design
- Public load balancer
- Web Tier
- Internal load balancer
- Application Tier
- Managed MySQL
- Read replica
- Main traffic flow

## Architecture Diagram

![Screenshot AD](screenshots/week-8-assign-5-architectural-diagram.png)

---

# Task 2 — Build the Terraform Networking and Security Layers

## Goal

Create the modular Terraform project and implement the network and security layers across the required public and private subnets.

## Evidence

### Screenshot 6 — Modular Terraform Project Structure

Add a screenshot showing the modular Terraform project structure.

![Screenshot 6](screenshots/week-8-assign-5-task-2-ss-6.png)

---

### Screenshot 7 — Six-Subnet Architecture

Add a screenshot showing the six-subnet architecture across two availability locations.

![Screenshot 7](screenshots/week-8-assign-5-task-2-ss-7.png)

---

### Screenshot 8 — Public and Private Tier Separation

Add a screenshot showing the public and private tier separation, including routing and security boundaries.

![Screenshot 8](screenshots/week-8-assign-5-task-2-ss-8.png)

---

# Task 3 — Build the Load-Balancing and Compute Layers

## Goal

Deploy the public and internal load balancers and the Web and Application compute resources required by the Book Review App.

## Evidence

### Screenshot 9 — Web and Application Compute

Add a screenshot showing the Web and Application compute resources in their required subnets.

![Screenshot 9](screenshots/week-8-assign-5-task-3-ss-9.png)

---

### Screenshot 10 — Public Load Balancer

Add a screenshot showing the internet-facing public load balancer.

![Screenshot 10](screenshots/week-8-assign-5-task-3-ss-10.png)

---

### Screenshot 11 — Internal Load Balancer

Add a screenshot showing the private internal load balancer.

![Screenshot 11](screenshots/week-8-assign-5-task-3-ss-11.png)

---

### Screenshot 12 — Healthy Targets

Add a screenshot showing healthy target groups or backend pools.

![Screenshot 12](screenshots/week-8-assign-5-task-3-ss-12.png)

---

# Task 4 — Build the Managed MySQL Database Layer

## Goal

Deploy a private, highly available managed MySQL database with a read replica and restrict database connectivity to the Application Tier.

## Evidence

### Screenshot 13 — Managed MySQL Database

Add a screenshot showing the managed MySQL database deployment.

![Screenshot 13](screenshots/week-8-assign-5-task-4-ss-13.png)

---

### Screenshot 14 — High Availability

Add a screenshot showing the Multi-AZ or high-availability configuration.

![Screenshot 14](screenshots/week-8-assign-5-task-4-ss-14.png)

---

### Screenshot 15 — Read Replica

Add a screenshot showing the read replica configuration.

![Screenshot 15](screenshots//week-8-assign-5-task-4-ss-15.png)

---

### Screenshot 16 — Private Database Access

Add a screenshot showing that the database is private and accepts MySQL traffic only from the Application Tier.

![Screenshot 16](screenshots/week-8-assign-5-task-4-ss-16.png)

---

# Task 5 — Validate, Review, and Apply the Terraform Configuration

## Goal

Validate the Terraform configuration, review the execution plan using both Agentic AI and human judgment, and apply the infrastructure changes only after all required checks pass.

## Evidence

### Screenshot 17 — Terraform Validation

Add a screenshot showing successful `terraform validate` output.

![Screenshot 17](screenshots/week-8-assign-5-task-5-ss-17.png)

---

### Screenshot 18 — Terraform Plan

Add a screenshot showing the Terraform plan output.

![Screenshot 18](screenshots/week-8-assign-5-task-5-ss-18.png)

---

### Screenshot 19 — Terraform Apply

Add a screenshot showing successful `terraform apply` completion.

![Screenshot 19](screenshots/week-8-assign-5-task-5-ss-19.png)

---

# Task 6 — Deploy and Configure the Book Review Application

## Goal

Deploy and configure the Book Review App across the Web, Application, and Database tiers and verify the complete application functionality.

## Evidence

### Screenshot 20 — Homepage

Add a screenshot showing the Book Review App homepage through the public endpoint.

![Screenshot 20](screenshots/week-8-assign-5-task-6-ss-21.png)

---

### Screenshot 21 — Login or Authentication

Add a screenshot showing successful login or authentication.

![Screenshot 21](screenshots/week-8-assign-5-task-6-ss-21.png)

---

### Screenshot 22 — Book Data

Add a screenshot showing the book listing or book details.

![Screenshot 22](screenshots/week-8-assign-5-task-6-ss-22.png)

---

### Screenshot 23 — Review Functionality

Add a screenshot showing the review functionality working successfully.

![Screenshot 23](screenshots/week-8-assign-5-task-6-ss-23.png)

---

### Screenshot 24 — Backend or API Evidence

Add a screenshot showing that the backend or API is working successfully.

![Screenshot 24](screenshots/week-8-assign-5-task-6-ss-24.png)

---

### Screenshot 25 — Database Reads and Writes

Add a screenshot showing successful database reads and writes.

![Screenshot 25](screenshots/week-8-assign-5-task-6-ss-25.png)

## Public Application URL

**Public Application URL / DNS:** http://book-review-dev-public-alb-867081177.us-east-2.elb.amazonaws.com

---

# Task 7 — Demonstrate the Agentic AI Workflow

## Goal

Demonstrate how Claude Code assisted with Terraform generation, architecture and security review, and evidence-based troubleshooting while infrastructure-changing decisions remained under human control.

You do not need to submit your complete Claude Code conversation history. Include only focused evidence.

## Evidence

### Screenshot 26 — AI-Assisted Terraform Generation

Add a screenshot showing one useful example of AI-assisted Terraform generation or improvement.

![Screenshot 26](screenshots/week-8-assign-5-task-7-ss-26.png)

---

### Screenshot 27 — Architecture or Security Review

Add a screenshot showing one structured architecture or security review result.

![Screenshot 27](screenshots/week-8-assign-5-task-7-ss-27.png)

---

### Screenshot 28 — AI-Assisted Troubleshooting

Add a screenshot showing one AI-assisted troubleshooting interaction based on collected evidence.

![Screenshot 28](screenshots/week-8-assign-5-task-7-ss-28.png)
---

# Task 8 — Complete the Final Architecture Review

## Goal

Review the completed infrastructure against the original capstone requirements and resolve significant architecture, security, reliability, and cost issues.

Confirm that the final review covers:

- Tier separation
- Availability
- Public exposure
- Routing
- Security rules
- Load balancing
- Database privacy
- Secrets
- Terraform quality
- Module structure
- Reliability
- Obvious cost risks

Use Screenshot 27 as the focused evidence for the structured architecture or security review.

---

# Task 9 — Answer the Reflection Questions

## Goal

Reflect on the architecture, Terraform implementation, and Agentic AI workflow. Answer each question briefly in your own words.

## Architecture

### 1. Why did you separate the Web, Application, and Database tiers?

 The three-tier architecture separates the responsibilities of the application and creates clear security boundaries.

The Web tier handles public HTTP traffic and serves the frontend. The Application tier contains the backend API and business logic. The Database tier stores persistent application data.

This separation makes the system easier to secure, troubleshoot, maintain, and scale. For example, the database does not need to be exposed to the Internet because only the Application tier needs to communicate with it.

### 2. Why is the Application Tier private?

The Application tier contains the backend API and business logic, so it does not need to receive requests directly from the public Internet.

Keeping it in private subnets reduces the attack surface. Requests follow a controlled path:

Internet → Public ALB → Web tier → Internal ALB → Application tier

This prevents users from directly accessing the backend EC2 instances.

### 3. Why is MySQL private?

The database contains persistent application information and should not be directly accessible from the Internet.

The RDS database is therefore placed in private database subnets, with access to MySQL port 3306 restricted to the Application tier.

This follows the principle of least privilege: only the component that needs database access should be allowed to connect to it.

### 4. Why are multiple Availability Zones used?

Multiple Availability Zones improve availability and resilience.

If resources are distributed across two Availability Zones, the failure of one Availability Zone does not necessarily make the entire application unavailable.

In this project, the Web, Application, and Database network design spans two Availability Zones to provide a more highly available architecture.

### 5. What is the difference between Multi-AZ/high availability and a read replica?

They solve different problems.

Multi-AZ/High Availability is primarily for resilience and failover. A standby database can take over if the primary database becomes unavailable.

A read replica is primarily for read scaling. It can handle read traffic separately from the primary database.

Therefore:

Multi-AZ → availability/failover
Read replica → read scalability

They are complementary rather than interchangeable.

Important: Before submitting this answer, make sure your deployed Terraform actually includes the assignment's required read replica. We have confirmed the Multi-AZ RDS configuration, but we had not yet established evidence that a read replica was actually deployed.

## Terraform

### 6. How did you divide your Terraform into modules?

I used Terraform modules to divide the infrastructure into logical components instead of putting everything into one large Terraform configuration.

The project uses modules for areas such as:

* Network
* Security
* Load balancing
* Compute
* Database

This improves organization, reuse, maintainability, and troubleshooting. It also makes it easier to understand which part of the infrastructure is responsible for a particular resource.

### 7. How do the modules communicate through variables and outputs?

Terraform modules communicate through input variables and outputs.

For example, the network module can create the VPC and subnets and expose their IDs through outputs. Other modules can then receive those values as inputs.

The same approach can be used for security-group IDs, subnet IDs, VPC IDs, and load-balancer information.

This avoids hardcoding resource IDs and creates dependencies between modules in a controlled way.

### 8. What did you specifically check in `terraform plan`?

Before applying Terraform changes, I reviewed the plan to understand what AWS resources Terraform intended to create, modify, or destroy.

I specifically looked for:

* Unexpected resource creation or deletion
* Public IP assignments
* Internet-facing resources
* 0.0.0.0/0 security rules
* Backend port 3001 exposure
* MySQL port 3306 exposure
* Whether the database was publicly accessible
* Changes that would replace existing resources
* Availability Zone distribution
* Load-balancer configuration
* Potential cost implications
* Dependencies between resources

This was important because Terraform should not be applied simply because the configuration successfully validates.

## Agentic AI

### 9. What was the purpose of `CLAUDE.md`?

CLAUDE.md provided Claude Code with the project's persistent instructions and architectural context.

It defined important requirements such as:

* The three-tier architecture
* Public Web tier
* Private Application tier
* Private Database tier
* Six-subnet design
* Load-balancer requirements
* Security boundaries
* Required ports
* Terraform conventions
* Security requirements
* Secret-handling rules
* Validation requirements
* Human approval for infrastructure-changing operations

This reduced the chance of Claude making recommendations that conflicted with the architecture or assignment requirements.

### 10. What work did the Terraform Engineer subagent perform?

The Terraform Engineer subagent was used to assist with Terraform-related engineering work.

Its responsibilities included helping with:

* Terraform module design
* Resource configuration
* Variables and outputs
* Terraform file creation and modification
* Infrastructure refactoring
* Terraform validation
* Provider and resource research

The subagent assisted with the implementation, but its output still required human review before infrastructure changes were approved.

### 11. What did the Architecture and Security Reviewer identify?

The Architecture and Security Reviewer identified several key alignment points and minor gaps across the networking and database modules:

Compliant Design (PASS): Verified that the VPC CIDR (10.0.0.0/16) matched specification, all six subnets (Web A/B, App A/B, DB A/B) were properly mapped across us-east-2a and us-east-2b, and strict public routing isolation was enforced (map_public_ip_on_launch = false for App and DB tiers with no direct internet routes).

Security & Configuration Findings (WARN/FAIL): Highlighted the need for explicit egress port restrictions on the DB tier security group, identified missing dynamic database secret generation controls, and flagged potential target group port mismatches between the internal ALB listener and the Express application instance on port 3001.

### 12. Why did you use Terraform MCP instead of relying only on Claude's existing Terraform knowledge?

I used the Terraform Model Context Protocol (MCP) server because relying solely on static LLM knowledge can lead to outdated provider syntax, deprecated parameter flags, and unvalidated module structures. Terraform MCP allowed Claude Code to:

* Query Live Provider Schemas: Retrieve exact argument definitions, required parameters, and valid attribute outputs directly from the current AWS provider schema.

* Validate Syntax in Real Time: Execute active validation checks against local .tf files during generation to catch syntax errors or missing required arguments before running terraform plan.

* Ensure State Awareness: Maintain context over state outputs and resource references across multi-tier modules (Network, App, Database) without halluncinating invalid resource parameters.

### 13. What was the purpose of your validation hooks?

The primary purpose of the validation hooks was to establish automated quality and security guardrails directly into the local workflow. Specifically, they were used to:

* Prevent Unsafe Terraform Commits: Automatically run terraform fmt and terraform validate to enforce uniform code styling and structural validity prior to staging changes.

* Enforce Security Safeguards: Execute static security scans to prevent hardcoded credentials, sensitive outputs, or overly permissive security group rules (0.0.0.0/0) from entering the deployment pipeline.

* Maintain Architectural Compliance: Verify that critical tags and naming conventions required by CLAUDE.md were present on newly generated infrastructure modules.

### 14. Describe one real issue Claude helped you troubleshoot.

Claude assisted in diagnosing a connection timeout error occurring when the Frontend (Web Tier) attempted to route API requests to the Backend (App Tier) via the Internal Application Load Balancer (ALB).

* The Problem: Direct local requests on the App Instance (10.0.11.198:3001) returned 200 OK, but requests sent through the Internal ALB timed out, preventing frontend API calls from reaching Express.

* Claude's Assistance: By analyzing collected evidence (curl outputs, security group rules, and log states), Claude identified that while the Internal ALB ingress rule correctly accepted traffic from the Web Tier, the App Tier security group was missing an ingress rule allowing inbound traffic from the Internal ALB Security Group on port 3001.

* The Resolution: Claude provided the exact aws_security_group_rule snippet targeting the Internal ALB security group ID, restoring the Web EC2 → Internal ALB → App EC2 network path.

### 15. Describe one recommendation you reviewed, modified, or rejected instead of accepting blindly.

* Claude's Initial Recommendation: During the initial database tier generation, Claude suggested configuring the RDS instance inside a public subnet with publicly_accessible = true and restricting access solely via Security Group IP whitelist rules to simplify early database migration testing.

* My Evaluation & Modification: I rejected the publicly_accessible = true suggestion because it violated core security requirements outlined in CLAUDE.md, which strictly mandate zero direct public IP exposure for database instances.

* The Action Taken: I modified the Terraform code to keep the RDS instance strictly confined to the private DB subnets (map_public_ip_on_launch = false). Instead of opening public database routes, I established administrative database access exclusively through the App Tier instance inside the internal VPC network.

---

# Task 10 — Publish the Mandatory LinkedIn Post

## Goal

Publish a LinkedIn post describing the capstone, the technical work completed, the Agentic AI workflow, and the lessons learned.

Write the post in your own words, include at least one project image or other proof, and ensure that it can be viewed by the submission reviewer.

## LinkedIn Post URL

**LinkedIn Post URL:** https://www.linkedin.com/posts/godwin-obi-008a12177_godwin-obi-dmi-cohort-3-live-activity-7504158271738621952-gEAH?utm_source=share&utm_medium=member_desktop&rcm=ACoAACn5hogBVyHnSR92cyBf5EzFBZEMSepEVPM

---

# Submission Instructions

- Complete Tasks 0–10 in sequence.
- Include all Screenshots 1–28 exactly as specified.
- Ensure that your full name is visible in the required screenshots.
- Include the selected cloud platform.
- Include the completed architecture diagram.
- Include the modular Terraform project structure.
- Include the working public application URL or public load-balancer DNS.
- Include all required Agentic AI workflow evidence.
- Answer all 15 reflection questions briefly in your own words.
- Include the published LinkedIn post URL.
- Do not expose cloud credentials, database passwords, SSH private keys, JWT secrets, access tokens, account IDs, Terraform state containing sensitive values, or other confidential information.
- Review all screenshots and project files carefully before submitting through GitHub.

---

# Completion Checklist

- [ ] Selected AWS or Azure
- [ ] Added and reviewed the Agentic AI starter files
- [ ] Configured `CLAUDE.md`
- [ ] Configured the Terraform Engineer subagent
- [ ] Configured the Architecture and Security Reviewer subagent
- [ ] Connected Terraform MCP
- [ ] Configured validation hooks and safety guardrails
- [ ] Created the architecture diagram
- [ ] Created the six-subnet design
- [ ] Configured public Web Tier routing
- [ ] Kept the Application Tier private
- [ ] Kept the Database Tier private
- [ ] Configured tier-specific Security Groups or NSGs
- [ ] Restricted backend port `3001`
- [ ] Restricted MySQL port `3306` to the Application Tier
- [ ] Created the public load balancer
- [ ] Created the internal load balancer
- [ ] Configured listeners and health checks
- [ ] Deployed the Web Tier compute resources
- [ ] Deployed the private Application Tier compute resources
- [ ] Provisioned private managed MySQL
- [ ] Configured Multi-AZ or high availability
- [ ] Configured a read replica
- [ ] Created the modular Terraform project
- [ ] Used variables, outputs, and module dependencies
- [ ] Used current Terraform documentation through MCP
- [ ] Used hooks for deterministic validation
- [ ] Completed `terraform fmt`
- [ ] Completed `terraform validate`
- [ ] Reviewed `terraform plan`
- [ ] Completed the Terraform Engineer review
- [ ] Completed the Architecture and Security review
- [ ] Applied the infrastructure only after human approval
- [ ] Deployed and configured the backend
- [ ] Deployed and configured the frontend
- [ ] Configured Nginx where required
- [ ] Configured the internal backend endpoint
- [ ] Configured the public frontend endpoint
- [ ] Verified the homepage
- [ ] Verified login or authentication
- [ ] Verified book data
- [ ] Verified review functionality
- [ ] Verified the backend API
- [ ] Verified database reads and writes
- [ ] Verified healthy load-balancer targets
- [ ] Included AI-assisted Terraform generation evidence
- [ ] Included one architecture or security review
- [ ] Included one AI-assisted troubleshooting example
- [ ] Completed the final architecture review
- [ ] Answered all 15 reflection questions
- [ ] Published the mandatory LinkedIn post
- [ ] Added the LinkedIn post URL
- [ ] Captured all 28 required screenshots
- [ ] Confirmed that my full name is visible in the required screenshots
- [ ] Checked that no secrets or sensitive information are exposed

---

## About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory), focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations through hands-on experience.

---

## Resources

- Book Review App Repository: [https://github.com/pravinmishraaws/book-review-app](https://github.com/pravinmishraaws/book-review-app)
- DMI Official Website: [https://dmi.pravinmishra.com](https://dmi.pravinmishra.com)
- University: [https://university.pravinmishra.com](https://university.pravinmishra.com)
- Discord Community: [https://discord.pravinmishra.com](https://discord.pravinmishra.com)
- Blog: [https://dmi.pravinmishra.com/blog](https://dmi.pravinmishra.com/blog)
- YouTube Playlist: [https://www.youtube.com/playlist?list=PLFeSNDtI4Cho](https://www.youtube.com/playlist?list=PLFeSNDtI4Cho)
- Pravin Mishra on LinkedIn: [https://www.linkedin.com/in/pravin-mishra-aws-trainer/](https://www.linkedin.com/in/pravin-mishra-aws-trainer/)
- CloudAdvisory on LinkedIn: [https://www.linkedin.com/company/thecloudadvisory/](https://www.linkedin.com/company/thecloudadvisory/)

---

*This submission is part of the DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
