# Assignment 5 — Deploy a Highly Available Two-Tier Application on AWS (VPC + ALB + ASG + Multi-AZ RDS)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will design and deploy a highly available two-tier web application on AWS: highly available networking across two Availability Zones, an Application Load Balancer, an Auto Scaling Group for the web tier, and a private Multi-AZ RDS database. You must prove high availability with real failure tests.

---

# Task 1 — Create HA Networking (VPC + 4 Subnets + IGW + NAT + Route Tables)

## Goal

Build a VPC (10.0.0.0/16) with two public and two private subnets across two Availability Zones, an Internet Gateway, a NAT Gateway, and the matching public/private route tables.

### Evidence

#### Screenshot 1 — VPC details showing CIDR 10.0.0.0/16

![Screenshot 1](screenshots/week-6-assign-5-task-1-ss-1.png)

---

#### Screenshot 2 — Subnets list showing four subnets and their Availability Zones

![Screenshot 2](screenshots/week-6-assign-5-task-1-ss-2.png)

---

#### Screenshot 3 — Public route table showing the Internet Gateway route and both public-subnet associations

![Screenshot 3](screenshots/week-6-assign-5-task-1-ss-3.png)

---

#### Screenshot 4 — Private route table showing the NAT Gateway route and both private-subnet associations

![Screenshot 4](screenshots/week-6-assign-5-task-1-ss-4.png)

---

#### Screenshot 5 — NAT Gateway status showing Available and the Elastic IP

![Screenshot 5](screenshots/week-6-assign-5-task-1-ss-5.png)

---

# Task 2 — Create Security Groups (ALB, EC2, RDS) with Least Privilege

## Goal

Create `ha-alb-sg` (HTTP public), `ha-web-sg` (HTTP only from `ha-alb-sg`, SSH from your IP), and `ha-db-sg` (database port only from `ha-web-sg`).

### Evidence

#### Screenshot 6 — ALB Security Group inbound rules

![Screenshot 6](screenshots/week-6-assign-5-task-2-ss-6.png)

---

#### Screenshot 7 — EC2 Security Group inbound rules showing the ALB Security Group reference and SSH from your IP

![Screenshot 7](screenshots/week-6-assign-5-task-2-ss-7.png)

---

#### Screenshot 8 — RDS Security Group inbound rule showing the database port allowed only from the EC2 Security Group

![Screenshot 8](screenshots/week-6-assign-5-task-2-ss-8.png)

---

# Task 3 — Deploy Database Tier (RDS Multi-AZ in Private Subnets)

## Goal

Launch a private, Multi-AZ RDS database (MySQL or PostgreSQL) using the private DB Subnet Group and `ha-db-sg`.

### Evidence

#### Screenshot 9 — RDS summary showing Multi-AZ = Yes and Publicly accessible = No

![Screenshot 9](screenshots/week-6-assign-5-task-3-ss-9.png)

---

#### Screenshot 10 — RDS connectivity section showing the DB Subnet Group and Security Group

![Screenshot 10](screenshots/week-6-assign-5-task-3-ss-10.png)

---

# Task 4 — Build a Launch Template (User Data Installs App + Connects to DB)

## Goal

Create a Launch Template whose user data installs the web-server runtime, deploys the application, configures the database connection, and starts the required services.

### Evidence

#### Screenshot 11 — Launch Template details showing that user data exists, including a visible snippet

![Screenshot 11](screenshots/week-6-assign-5-task-4-ss-11.png)

---

#### Screenshot 12 — A running instance created from the template showing that the application responds on port 80 through a local test or browser using its public IP

![Screenshot 12](screenshots/week-6-assign-5-task-4-ss-12.png)

---

# Task 5 — Create an Application Load Balancer (ALB) Across 2 Public Subnets

## Goal

Create an internet-facing ALB across both public subnets with an HTTP listener and a healthy instance target group.

### Evidence

#### Screenshot 13 — ALB details showing two public subnets in two Availability Zones

![Screenshot 13](screenshots/week-6-assign-5-task-5-ss-13.png)

---

#### Screenshot 14 — Target group showing at least one healthy target

![Screenshot 14](screenshots/week-6-assign-5-task-5-ss-14.png)

---

# Task 6 — Create Auto Scaling Group (ASG) in 2 Public Subnets

## Goal

Create an Auto Scaling Group from the Launch Template across both public subnets, with desired capacity 2, minimum 2, and maximum 4, registered to the ALB target group.

### Evidence

#### Screenshot 15 — Auto Scaling Group showing desired, minimum, and maximum capacity and the selected subnet Availability Zones

![Screenshot 15](screenshots/week-6-assign-5-task-6-ss-15.png)

---

#### Screenshot 16 — EC2 instances list showing two running instances in different Availability Zones

![Screenshot 16](screenshots/week-6-assign-5-task-6-ss-16.png)

---

# Task 7 — Configure App to Use RDS + Validate Read/Write

## Goal

Confirm the application communicates with the RDS database through the ALB DNS name with at least one read and one write operation.

### Evidence

#### Screenshot 17 — Browser showing the application loaded through the ALB DNS name with the URL visible

![Screenshot 17](screenshots/week-6-assign-5-task-7-ss-17.png)

---

#### Screenshot 18 — Proof of a database write through a UI message or database query output

![Screenshot 18](screenshots/week-6-assign-5-task-7-ss-18.png)

---

# Task 8 — High Availability Tests (Must Do Both)

## Goal

Test A: terminate one web instance and confirm the Auto Scaling Group replaces it automatically without interrupting the ALB.

Test B: simulate an Availability Zone impact (stop, detach, or reduce desired capacity in one AZ) and confirm the application stays available.

### Evidence

#### Screenshot 19 — EC2 showing the terminated instance and the newly launched instance; timestamps are helpful

![Screenshot 19](screenshots/week-6-assign-5-task-8-ss-19.png)

---

#### Screenshot 20 — Target group showing healthy targets after replacement

![Screenshot 20](screenshots/week-6-assign-5-task-8-ss-20.png)

---

#### Screenshot 21 — Evidence that an instance was removed, detached, placed in Standby, or stopped in one Availability Zone

![Screenshot 21](screenshots/week-6-assign-5-task-8-ss-21.png)

---

#### Screenshot 22 — Browser showing that the ALB DNS endpoint still works during the change

![Screenshot 22](screenshots/week-6-assign-5-task-8-ss-22.png)

---

# Task 9 — Architecture and Test-Results Summary

## Goal

Summarize the VPC/subnet layout, the ALB and Auto Scaling Group setup, the private Multi-AZ RDS setup, and the results of both high-availability tests.

### Evidence

#### Screenshot 23 — A simple architecture diagram, which may be hand-drawn, or an AWS console overview showing the components

![Screenshot 23](screenshots/week-6-assign-5-task-9-ss-23.png)

---

### Notes

Summarize the VPC and subnets across the two Availability Zones.

* **VPC:** ha-vpc configured across two Availability Zones (eu-north-1a and eu-north-1b).

* **Public Subnets:** public-subnet-A and public-subnet-B hosting the Application Load Balancer and NAT Gateways/public EC2 interfaces.

* **Private Subnets:** private-subnet-A and private-subnet-B hosting the application web instances and database subnet group.

* **Routing & Security:** Public subnets route outbound internet traffic via an Internet Gateway. Private subnets route via NAT Gateways for secure outbound updates. Security Groups enforce strict tier isolation (ALB $\rightarrow$ EC2 $\rightarrow$ RDS).

Summarize the ALB and Auto Scaling Group setup.

* **Application Load Balancer (ALB):** Named ha-alb, deployed as internet-facing across both public subnets (public-subnet-A and public-subnet-B).

* **Target Group:** ha-web-tg using HTTP on Port 80 with health checks monitoring root path HTTP responses.

* **Auto Scaling Group (ASG):** Named ha-asg, using ha-web-template.

* **Capacity Settings:** Desired capacity = 2, Minimum capacity = 2, Maximum capacity = 4.

* **Distribution:** Spans both public subnets across eu-north-1a and eu-north-1b attached to ha-web-tg to ensure seamless dynamic load balancing and auto-healing.

Summarize the private Multi-AZ RDS setup.

* **Database Instance:** Named ha-db, running MySQL engine version 8.0.

* **Deployment Option:** Multi-AZ deployment (creates a primary DB instance in one AZ and a synchronous standby replica in a second AZ for failover protection).

* **Subnet Group:** ha-db-subnet-group consisting strictly of private subnets (private-subnet-A and private-subnet-B).

* **Public Accessibility:** Set to No (accessible only within the VPC from instances attached to HA-EC2-Security-Group on port 3306).

Summarize the results of both high-availability tests.

* **Test A (Single Instance Termination):**

    * **Result:** SUCCESS. Terminating a running web instance triggered the Auto Scaling Group health check. The ASG automatically launched a replacement instance to maintain the desired capacity of 2. The Application Load Balancer seamlessly routed traffic to the remaining healthy instance without causing application downtime.

* **Test B (Availability Zone Impact Simulation):**

    * **Result:** SUCCESS. Simulating an AZ disruption (removing/detaching an instance in one AZ) demonstrated that the ALB continued serving user requests via the target in the remaining healthy AZ. The ASG rebalanced instances across available zones, and database state persisted independently on the Multi-AZ RDS backend.

---

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post about the high-availability build, including the ALB URL (or a redacted screenshot), three to five lines on what you built and how you tested high availability, and one proof screenshot.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/godwin-obi-008a12177_dmi-devops-micro-internship-with-agentic-share-7494188027200663552-qXde/?utm_source=share&utm_medium=member_desktop&rcm=ACoAACn5hogBVyHnSR92cyBf5EzFBZEMSepEVPM`

---

#### Screenshot of LinkedIn post

![Screenshot 24](screenshots/week-6-assign-5-linkedIn-post.png)

---

# Submission Instructions

- Add all required screenshots in your submission
- Do not expose passwords, connection strings, private keys, or account IDs

---

# Completion Checklist

- [ ] Task 1: VPC, four subnets, IGW, NAT Gateway, and route tables created (Screenshots 1–5)
- [ ] Task 2: Least-privilege ALB, EC2, and RDS security groups created (Screenshots 6–8)
- [ ] Task 3: Private Multi-AZ RDS created (Screenshots 9–10)
- [ ] Task 4: Self-configuring Launch Template created and tested (Screenshots 11–12)
- [ ] Task 5: ALB created across both public subnets (Screenshots 13–14)
- [ ] Task 6: Auto Scaling Group running two instances across two AZs (Screenshots 15–16)
- [ ] Task 7: Application verified through the ALB with a database read and write (Screenshots 17–18)
- [ ] Task 8: Both high-availability tests completed (Screenshots 19–22)
- [ ] Task 9: Architecture and test-results summary completed (Screenshot 23 & Notes)
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

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