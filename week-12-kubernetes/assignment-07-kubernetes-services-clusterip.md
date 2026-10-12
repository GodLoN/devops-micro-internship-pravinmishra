# Assignment 7 — Kubernetes Services (ClusterIP)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this guided lab, you will create an internal ClusterIP Service for NGINX, call it by DNS and virtual IP, break and fix its selector, and prove readiness-aware endpoint routing.

---

# Task 1 — Deploy the Probed NGINX Workload

## Goal

Create two healthy, labeled NGINX Pods (readiness + liveness probes) as Service backends.

### Evidence

#### Screenshot 1 — Two Ready Pods with labels and IPs

![Screenshot 1](screenshots/week-12-assign-7-task-1-ss-1.png)

---

# Task 2 — Create and Inspect the ClusterIP Service

## Goal

Create `nginx-svc` (type `ClusterIP`, selector `app: nginx`, port 80) and inspect the Service, Endpoints, and EndpointSlices.

### Evidence

#### Screenshot 2 — Service ClusterIP plus populated Endpoints and EndpointSlices

![Screenshot 2](screenshots/week-12-assign-7-task-2-ss-2.png)

---

# Task 3 — Call the Service from a Client Pod

## Goal

Create a BusyBox `tester` Pod and call `nginx-svc` by short name, ClusterIP, and both short/FQDN via `nslookup`.

### Evidence

#### Screenshot 3 — Successful `wget` responses and `nslookup` output

![Screenshot 3](screenshots/week-12-assign-7-task-3-ss-3.png)

---

# Task 4 — Break and Fix the Selector Contract

## Goal

Change the Service selector to `app: does-not-match`, confirm endpoints become empty and requests fail, then restore `app: nginx`.

### Evidence

#### Screenshot 4 — Empty endpoints during failure and restored endpoints after the fix

![Screenshot 4](screenshots/week-12-assign-7-task-4-ss-4.png)

---

# Task 5 — Prove Readiness-Aware Routing

## Goal

Scale to one replica, apply a broken readiness patch, confirm the NotReady Pod is excluded from Service endpoints, then restore the healthy Deployment.

### Evidence

#### Screenshot 5 — NotReady Pod with excluded endpoint, followed by restored endpoint membership

![Screenshot 5](screenshots/week-12-assign-7-task-5-ss-5.png)

---

# Task 6 — Troubleshoot and Optionally Clean Up

## Goal

Verify the Service path, then optionally delete `tester` and `nginx-svc`.

### Evidence

#### Screenshot 6 — Final verification or optional cleanup output

![Screenshot 6](screenshots/week-12-assign-7-task-6-ss-6.png)

---

### Notes

Write a short note describing what the lab demonstrated.

This lab demonstrated how a Kubernetes ClusterIP Service provides stable internal access to changing Pods. I deployed two NGINX replicas with readiness and liveness probes, created a ClusterIP Service, and verified its endpoints and EndpointSlice. From a tester Pod, I accessed NGINX using the Service DNS name and ClusterIP and confirmed DNS resolution. I deliberately broke the Service selector and observed that the endpoints disappeared and requests failed. After restoring the selector, connectivity returned. Finally, I broke the readiness probe and verified that the NotReady Pod was marked `ready: false` in the EndpointSlice while the healthy Pods continued serving traffic. I restored the healthy configuration and verified the Service again. I learned that labels and selectors enable service discovery, Services provide stable internal addresses, and readiness probes help prevent traffic from being routed to unready application instances.

---

# Submission Instructions

- Add all required screenshots in your submission
- Include the completed YAML manifests used in the lab

---

# Completion Checklist

- [ ] Task 1: Probed NGINX Deployment applied (Screenshot 1)
- [ ] Task 2: ClusterIP Service created and inspected (Screenshot 2)
- [ ] Task 3: Service reached by DNS and ClusterIP (Screenshot 3)
- [ ] Task 4: Selector broken and fixed (Screenshot 4)
- [ ] Task 5: Readiness-aware routing proven (Screenshot 5)
- [ ] Task 6: Verified / cleaned up (Screenshot 6)
- [ ] Reflection notes written (Notes)

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
