# Assignment 6 — Deploy the Book Review App with Docker Compose

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will deploy the Book Review Application with Docker Compose using MySQL, a backend API, and a frontend user interface. You will configure health-gated startup, browser-facing API access, CORS, and persistent MySQL storage.

---

# Task 1 — Prepare the Project

## Goal

Prepare your fork of the Book Review App repository for Docker Compose deployment.

### Evidence

#### Screenshot 1 — Project Structure

Add a screenshot showing the project structure containing:

```text
frontend/
backend/
.env.example
.gitignore
docker-compose.yml
```

![Screenshot 1](screenshots/week-11-assign-6-task-1-ss-1.png)

---

#### Screenshot 2 — Environment and Docker Ignore Files

Add a screenshot showing the contents of:

```text
.env.example
.gitignore
frontend/.dockerignore
backend/.dockerignore
```

Ensure that no real passwords, tokens, or secrets are visible.

![Screenshot 2](screenshots/week-11-assign-6-task-1-ss-2.png)

---

# Task 2 — Create or Confirm Application Dockerfiles

## Goal

Prepare Dockerfiles for the frontend and backend services and build both services through Docker Compose.

### Evidence

#### Screenshot 3 — Frontend Dockerfile

Add a screenshot showing the completed `frontend/Dockerfile`.

![Screenshot 3](screenshots/week-11-assign-6-task-2-ss-3.png)

---

#### Screenshot 4 — Backend Dockerfile

Add a screenshot showing the completed `backend/Dockerfile`.

![Screenshot 4](screenshots/week-11-assign-6-task-2-ss-4.png)

---

#### Screenshot 5 — Docker Compose Build

Add a screenshot of the terminal showing successful completion of:

```bash
docker compose build
```

![Screenshot 5](screenshots/week-11-assign-6-task-2-ss-5.png)

---

# Task 3 — Create the Docker Compose Stack

## Goal

Create one `docker-compose.yml` file that builds and runs MySQL, backend, and frontend services.

### Evidence

#### Screenshot 6 — MySQL Service, Health Check, and Volume Mount

Add a screenshot showing the MySQL service in `docker-compose.yml`, including:

- MySQL image
- Environment variables
- MySQL health check
- `mysql_data` volume mount
- No published MySQL port

![Screenshot 6](screenshots/week-11-assign-6-task-3-ss-6.png)

---

#### Screenshot 7 — Backend Configuration

Add a screenshot showing the backend service configuration, including:

- `depends_on` with `condition: service_healthy`
- Database host set to `mysql`
- Browser frontend origin configured for CORS
- Published backend port

![Screenshot 7](screenshots/week-11-assign-6-task-3-ss-7.png)

---

#### Screenshot 8 — Frontend Configuration

Add a screenshot showing the frontend service configuration, including:

- Published frontend port
- `depends_on` for the backend service
- Browser-facing `NEXT_PUBLIC_API_URL`

![Screenshot 8](screenshots/week-11-assign-6-task-3-ss-8.png)

---

#### Screenshot 9 — Named Volume Definition

Add a screenshot showing the `mysql_data` volume definition in `docker-compose.yml`.

![Screenshot 9](screenshots/week-11-assign-6-task-3-ss-9.png)

---

# Task 4 — Start and Verify the Stack

## Goal

Build and start all services through one Docker Compose workflow.

### Evidence

#### Screenshot 10 — Docker Compose Service Status

Add a screenshot of the terminal showing:

```bash
docker compose ps
```

The output must show the MySQL, backend, and frontend services running. MySQL must show as healthy.

![Screenshot 10](screenshots/week-11-assign-6-task-4-ss-10.png)

---

#### Screenshot 11 — MySQL and Backend Logs

Add a screenshot of the terminal showing:

```bash
docker compose logs mysql backend --tail=50
```

The logs must show MySQL readiness and successful backend database connection.

![Screenshot 11](screenshots/week-11-assign-6-task-4-ss-11.png)

---

# Task 5 — Test End-to-End Application Functionality

## Goal

Verify that the Book Review App works through the browser.

### Evidence

#### Screenshot 12 — Successful Registration or Login

Add a browser screenshot showing successful user registration or login.

Add your full name as a clear caption directly below the screenshot.

![Screenshot 12](screenshots/week-11-assign-6-task-5-ss-12.png)

---

#### Screenshot 13 — Created Book Review

Add a browser screenshot showing a created book review visible in the application.

Add your full name as a clear caption directly below the screenshot.

![Screenshot 13](screenshots/week-11-assign-6-task-5-ss-13.png)

---

#### Screenshot 14 — CORS Verification

Add a browser developer-tools screenshot with:

- The Network tab showing a successful API request
- The Console drawer showing no CORS error after the API interaction

![Screenshot 14](screenshots/week-11-assign-6-task-5-ss-14.png)

---

# Task 6 — Prove MySQL Data Persistence

## Goal

Verify that MySQL data remains after a non-destructive Docker Compose down/up cycle.

### Evidence

#### Screenshot 15 — Data Before Restart

Add a browser screenshot showing the registered user or created review before the down/up cycle.

Add your full name as a clear caption directly below the screenshot.

![Screenshot 15](screenshots/week-11-assign-6-task-6-ss-15.png)

---

#### Screenshot 16 — Non-Destructive Stack Restart

Add a screenshot of the terminal showing the non-destructive shutdown and restart:

```bash
docker compose down
docker compose up -d
docker compose ps
```

Do not use `docker compose down -v`.

![Screenshot 16](screenshots/week-11-assign-6-task-6-ss-16.png)

---

#### Screenshot 17 — Data After Restart

Add a browser screenshot showing the same registered user or review after the stack restarts.

Add your full name as a clear caption directly below the screenshot.

![Screenshot 17](screenshots/week-11-assign-6-task-6-ss-17.png)

---

# Task 7 — Explain Docker Compose Teardown Modes

## Goal

Explain the difference between preserving data and fully resetting a Docker Compose environment.

### Notes

Write a short explanation of 5–8 lines covering:

- What `docker compose down` removes and preserves
- Why named volumes should be kept when preserving MySQL data
- What happens when named volumes are removed
- When a full reset is useful
- Why a full reset must not be used before persistence evidence is captured

`docker compose down` stops and removes the Compose containers and network but preserves named volumes by default.

Because the MySQL data is stored in the named `mysql_data` volume, the database contents remain available after the containers are recreated.

`docker compose down -v` additionally removes the named volumes and permanently deletes the stored database data.

Using `down -v` is useful when a completely clean environment or database reset is required.
However, it must not be used before a persistence test because it would remove the very data we need to prove was preserved.

For this assignment, `docker compose down` followed by `docker compose up -d` demonstrated that the user and review data survived the container restart.


---

# Final Public Frontend URL

**Frontend URL:** `http://13.58.78.80:3000`

Replace the placeholder with your working application URL.

---

# GitHub Repository URL

**Your Fork or Repository URL:** `https://github.com/GodLoN/book-review-app.git`

---

# LinkedIn Requirement

## Goal

Create a LinkedIn post about the Book Review App deployment and what you learned from using Docker Compose.

### Evidence

**LinkedIn Post URL:** `https://www.linkedin.com/posts/godwin-obi-008a12177_devops-docker-dockercompose-activity-7511113483501891584-WH30?utm_source=share&utm_medium=member_desktop&rcm=ACoAACn5hogBVyHnSR92cyBf5EzFBZEMSepEVPM`

#### LinkedIn Post Screenshot

![Screenshot 18](screenshots/week-11-assign-6-linkedin-post-ss-18.png)

---

# Submission Checklist

- [ ] Book Review App repository forked and used
- [ ] `.env` excluded from Git tracking
- [ ] `.env.example` contains only safe placeholder values
- [ ] Frontend and backend Dockerfiles created or confirmed
- [ ] MySQL health check configured
- [ ] Backend waits for healthy MySQL
- [ ] Backend uses `mysql` as the database hostname
- [ ] Frontend API URL uses the VM public IP and backend port
- [ ] Backend CORS origin matches the frontend origin
- [ ] MySQL port 3306 is not publicly exposed
- [ ] Registration and login work
- [ ] Book review creation works
- [ ] Data persists after a non-destructive down/up cycle
- [ ] Screenshots 1–17 included
- [ ] Teardown explanation completed
- [ ] Public frontend URL included
- [ ] GitHub repository URL included
- [ ] LinkedIn post URL and screenshot included
- [ ] Full name visible in required terminal screenshots
- [ ] Browser screenshots include a full-name caption
- [ ] No sensitive information exposed

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

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
