# Assignment 6 — Capstone: Deploy Book Review App (Three-Tier Architecture) on Azure

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

This is the most important assignment of the course. You will deploy the Book Review App in a production-ready, best-practice-compliant three-tier architecture on Azure: separated presentation, application, and database tiers, least-privilege network access, a controlled public entry point, protected secrets, and availability/monitoring evidence.

---

# Task 1 — Design the Azure Three-Tier Architecture

## Goal

Create an architecture diagram and implementation plan identifying the presentation, application, and database components, the chosen Azure services, the public entry point, and the internal traffic paths.

### Evidence

#### Screenshot 1 — Architecture diagram showing the public entry point, three tiers, network boundaries, and traffic flow

![screenshot 01](screenshots/task6-screenshot-01.PNG)

---

#### Screenshot 2 — Written architecture assumptions and selected Azure services

![screenshot 02](screenshots/task6-screenshot-02.PNG)

---

# Task 2 — Create the Azure Network Foundation

## Goal

Create a dedicated Resource Group and VNet with separate subnets for the web, application, and database tiers, keeping the application and database tiers without direct public access.

### Evidence

#### Screenshot 3 — Resource Group overview showing the assignment resources

![screenshot 03](screenshots/task6-screenshot-03.PNG)

---

#### Screenshot 4 — VNet overview showing the address space and all required subnets

![screenshot 04](screenshots/task6-screenshot-04.PNG)

---

#### Screenshot 5 — Route-table or Private DNS evidence where applicable

![screenshot 05](screenshots/task6-screenshot-05.PNG)

---

# Task 3 — Configure Security and Secret Management

## Goal

Apply least-privilege NSG rules so traffic flows Internet → public entry point → web tier → application tier → database tier, and store credentials in Azure Key Vault or another approved secure mechanism.

### Evidence

#### Screenshot 6 — NSG rules proving least-privilege access between the tiers

![screenshot 06](screenshots/task6-screenshot-06.PNG)

![screenshot 06](screenshots/task6-screenshot-06ii.PNG)

---

#### Screenshot 7 — Key Vault or approved secret-management configuration (without displaying secret values)

![screenshot 07](screenshots/task6-screenshot-07.PNG)

---

# Task 4 — Deploy the Presentation (Web) Tier

## Goal

Deploy the Book Review App presentation layer on the approved web-tier compute service, configured to route requests to the internal application-tier endpoint, and not directly exposed except through the public entry service.

### Evidence

#### Screenshot 8 — Web-tier compute overview showing subnet and availability configuration

![screenshot 08](screenshots/task6-screenshot-08.PNG)

---

#### Screenshot 9 — Terminal or service output proving the presentation layer is running

![screenshot 09](screenshots/task6-screenshot-09.PNG)

---

# Task 5 — Deploy the Business (Application) Tier

## Goal

Deploy the Book Review App backend privately in the application subnet, configured to use the private database endpoint and secured environment values, reachable only through its internal endpoint.

### Evidence

#### Screenshot 10 — Application-tier compute overview showing private subnet placement

![screenshot 10](screenshots/task6-screenshot-10.PNG)

---

#### Screenshot 11 — Backend process, service, or listening-port evidence

![screenshot 11](screenshots/task6-screenshot-11.PNG)

---

#### Screenshot 12 — Internal health-check or API response (without exposing secrets)

![screenshot 12](screenshots/task6-screenshot-12.PNG)

---

# Task 6 — Deploy the Managed Database Tier

## Goal

Create a private Azure managed database (public access disabled), with availability/backup/retention settings, the Book Review App schema imported, and access restricted to the application tier only.

### Evidence

#### Screenshot 13 — Database overview showing private connectivity and public access disabled

![screenshot 13](screenshots/task6-screenshot-13.PNG)

---

#### Screenshot 14 — Availability, backup, and retention configuration

![screenshot 14](screenshots/task6-screenshot-14.PNG)

---

#### Screenshot 15 — Successful schema or connectivity verification (without exposing credentials)

![screenshot 15](screenshots/task6-screenshot-15.PNG)

---

# Task 7 — Configure Traffic Management, Availability, and Monitoring

## Goal

Configure the approved public entry service with health probes and backend pools, internal routing for the application tier where required, and enable Azure Monitor/diagnostics/logs/alerts for the key resources.

### Evidence

#### Screenshot 16 — Public entry service showing listener, frontend endpoint, and healthy web targets

![screenshot 16](screenshots/task6-screenshot-16.PNG)

---

#### Screenshot 17 — Internal application-tier load-balancing or routing configuration where applicable

![screenshot 17](screenshots/task6-screenshot-17.PNG)

---

#### Screenshot 18 — Azure Monitor, diagnostic settings, logs, metrics, or alert evidence

![screenshot 18](screenshots/task6-screenshot-18.PNG)

---

# Task 8 — Validate the Production-Style Deployment

## Goal

Confirm the Book Review App works end to end through the public endpoint, with at least one database read and one write, confirm private tiers are not internet-reachable, and complete a safe availability test.

### Evidence

#### Screenshot 19 — Browser showing the Book Review App through the public endpoint

![screenshot 19](screenshots/task6-screenshot-19.PNG)

---

#### Screenshot 20 — Proof of successful database-backed read and write operations

![screenshot 20](screenshots/task6-screenshot-20.PNG)

---

#### Screenshot 21 — Evidence that private tiers are not publicly accessible

![screenshot 21](screenshots/task6-screenshot-21.PNG)

---

#### Screenshot 22 — Availability-test and healthy-target evidence

![screenshot 22](screenshots/task6-screenshot-22.PNG)

---

#### Public Endpoint

Paste your public endpoint URL here:

`http://30.164.108.125/`

---

### Notes

Summarize what worked, issues encountered and how they were fixed, and the availability/security/secrets/monitoring/backup choices made.

What Worked

I successfully deployed the Book Review application using a three-tier Azure architecture. The Application Gateway is the only public entry point, while the web, application, and database tiers remain private. I also configured load balancing with multiple instances and tested failover by stopping one web instance. The application continued serving traffic through the healthy instance.

Issues Encountered and Fixes
Managed Identity: Subscription policy blocked the system-assigned identity, so I used a User-Assigned Managed Identity instead.
Private subnet connectivity: Package installation failed because the private subnets had no outbound access. I resolved this by adding a NAT Gateway.
Database connection: An environment variable containing # caused the password to be interpreted incorrectly. Quoting the value fixed the authentication issue.
Frontend API access: The frontend could not reach the private backend Load Balancer from a browser. I fixed this by routing API requests through the public Nginx endpoint.
CORS: Browser requests were blocked because the application expected an explicit allowed origin. I configured the Application Gateway public endpoint as the allowed origin.
Azure CLI on Windows: Some commands were affected by Git Bash path conversion. Using MSYS_NO_PATHCONV=1 resolved the issue.
Availability, Security, Secrets, Monitoring & Backup
Availability: Web and application tiers use multiple instances behind health-checked load balancers, and I verified failover during testing.
Security: NSGs restrict communication between tiers, and the web, app, and database servers have no public IPs.
Secrets: Database credentials are stored securely in Azure Key Vault instead of being hardcoded in the application.
Monitoring: Azure Monitor/Log Analytics is used to collect application and infrastructure logs and monitor unhealthy backends.
Backup: MySQL automated backups are enabled with a defined retention period to support recovery when needed.

---

# Submission Instructions

- Add all required screenshots and links in your submission
- Do not expose passwords, keys, connection strings, or subscription IDs

---

# Completion Checklist

- [ ] Task 1: Architecture diagram and assumptions documented (Screenshots 1–2)
- [ ] Task 2: Network foundation created with isolated tiers (Screenshots 3–5)
- [ ] Task 3: Least-privilege security and secret management configured (Screenshots 6–7)
- [ ] Task 4: Presentation tier deployed (Screenshots 8–9)
- [ ] Task 5: Application tier deployed privately (Screenshots 10–12)
- [ ] Task 6: Managed database tier deployed privately (Screenshots 13–15)
- [ ] Task 7: Public entry, internal routing, and monitoring configured (Screenshots 16–18)
- [ ] Task 8: End-to-end validation and availability test completed (Screenshots 19–22, Public Endpoint, Notes)
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

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
