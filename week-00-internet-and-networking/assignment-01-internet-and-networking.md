# Week 00 - Internet and Networking

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

# 🧑‍💻 Task 1: Using ChatGPT as Your Learning Assistant

## Scenario

You're new to DevOps and will frequently encounter technical questions. ChatGPT can be your learning companion.

## Your Task

Write a clear ChatGPT prompt to help you understand:

> "What is a protocol in networking? Explain with a simple real-life example."

Take a screenshot of your interaction showing:

* Your detailed prompt (with clear expectations)
* ChatGPT's simplified response with an example

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![Task 1 Screenshot](screenshots/task-1-chatgpt.png)


Replace `task-1-chatgpt.png` with your actual screenshot file name.

---

## What I Learned (2–3 lines)

I used was ChatGPT as a learning assistant, which broke down complex networking and system design concepts into simple, real-world explanations.

---

# 🌐 Task 2: Internet and Networking

## Scenario

Your friend is launching an online bookstore named **EpicReads**.

He asked you to explain how users globally can access his website hosted in Finland.

## Your Task

Write a short explanation (**100–150 words**) that includes:

* Packet Switching
* IP Address
* TCP/IP
* HTTP/HTTPS

💡 **Tip:** You may use ChatGPT (as demonstrated in Task 1) to refine your explanation.

## Answer

When someone visits EpicReads from anywhere in the world, their device sends a request over the internet using TCP/IP, the core communication protocol. The request is broken into small pieces through packet switching, allowing data to travel efficiently across different routes. Each packet carries the IP address of the user’s device and the IP address of your server in Finland, ensuring it reaches the correct destination. Once the packets arrive, they are reassembled into the original request. The website is then delivered back to the user using HTTP or the more secure HTTPS, which encrypts the data for safe transmission. This entire process happens within seconds, allowing users globally to access EpicReads seamlessly and securely.

---

# 🏗️ Task 3: Application Architecture & Stack

## Scenario

EpicReads bookstore has two application versions:

### Two-Tier Application

* Frontend
* Database

### Three-Tier Application

* Frontend
* Backend
* Database

## Your Task

* Draw simple diagrams (hand-drawn or tool-based such as draw.io)
* Label each layer clearly
* List at least two common technologies or tools used for each layer
* Submit a screenshot or photo clearly showing your own drawing

## Diagram Screenshot / Photo

Save your diagram image in the `screenshots` folder and update the file name below.

![Application Architecture Diagram](screenshots/task-3-diagram.png)


Replace `task-3-diagram.png` with your actual diagram file name.

---

## Technologies Used

### Frontend

* React/Next.js.
* Vue.js/Angular.

### Backend

* Node.js/Express.
* Django/FastAPI.

### Database

* PostgreSQL/MySQL.
* MongoDB.

---

# 🌍 Task 4: Domain Name & DNS (Basic Concepts)

## Scenario

Your friend's bookstore **EpicReads** is currently accessible through:

```text
52.172.142.222:3000
```

He purchased the domain:

```text
epicreads.com
```

## Your Task

In **50–100 words**, explain in your own words:

1. What is DNS (Domain Name System)?
2. Which DNS record type should be used to connect the domain to the given IP, and why?

## Answer

1.      What is DNS?
DNS (Domain Name System) is the Internet's phone book. When you type a website name like `epicreads.com` into your browser, your computer doesn't actually understand names; it only understands IP addresses (like “52.172.142.222”). DNS translates the human-friendly domain name into the numeric IP address so your browser knows exactly which server to connect to. Without DNS, everyone would have to memorize IP addresses to visit websites, so DNS makes it easier for use to visit websites.
2.      Which DNS record type to use?
You should use an A Record (Address Record): An A record directly maps a domain name to an IPv4 address. So, you'd create an A record pointing `epicreads.com` → `52.172.142.222`. This tells DNS servers worldwide: "whenever someone requests epicreads.com, send them to that IP." Since the IP given (“52.172.142.222”) is a standard IPv4 address, the A record is the correct and most straightforward choice, as opposed to a CNAME (which maps a domain to a domain, not to an IP) or an AAAA record (which is for IPv6 addresses).

---

# 💻 Task 5: Visual Studio Code Setup (Hands-on)

## Your Task

Install Visual Studio Code (if not already installed).

Take a screenshot of your VS Code environment showing:

* Terminal open inside VS Code
* Running a basic command:

### Windows

```powershell
dir
```

### Linux / macOS

```bash
pwd
ls
```

* Your selected VS Code theme clearly visible

⚠️ **Important:** The screenshot must show your username or another identifiable detail to confirm it is your environment.

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![VS Code Setup Screenshot](screenshots/task-5-vscode.png)


Replace `task-5-vscode.png` with your actual screenshot file name.

---

# 🔗 Task 6: Publish Your Assignment as a LinkedIn Post

## Objective

Publishing on LinkedIn helps you:

* Build your professional online presence
* Reinforce your learning
* Document your DevOps journey publicly

## Your Task

Summarize your answers from Tasks 1–5 into a LinkedIn post.

Clearly structure your post into the following sections:

* ChatGPT
* Internet & Networking
* App Architecture
* DNS
* VS Code Setup

Add the following credit note at the end of your post:

> **P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=cohort3**

---

## LinkedIn Post URL

Paste your LinkedIn post URL here:

```text
https://www.linkedin.com/posts/zahra-u-nura_dmi-share-7455333545524277248-Q2c8/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABhheJ4Bw5LI3hMBUfCD5MZiGRXdKYKjr0U
```

---

## LinkedIn Post Backup Copy

Paste the full text of your LinkedIn post here:

🚀 Here is My DevOps Learning Journey – and I'm already connecting dots:
Here's a summary of what I explored this week through an introductory DevOps Micro-Internship. One of the most impactful tools I used was ChatGPT as a learning assistant, which broke down complex networking and system design concepts into simple, real-world explanations.

🌐 Internet & Networking
Had to revisit the fundamentals of networking and how users access a global website using TCP/IP, packet switching, and IP addresses, with HTTP/HTTPS enabling secure communication between clients and servers.

🏗️ Application Architecture
I explore application architecture as it is built using multiple layers, each with a clear responsibility:
I also created simple diagrams (draw.io) to visualize the layers:
Frontend: React, HTML, CSS
Backend: Node.js, Python (Flask/Django), .NET
Database: PostgreSQL, MySQL, MongoDB
This helped me clearly understand how responsibilities are separated and why three-tier architectures are more scalable and secure.

🌍 DNS
I worked on mapping a domain to a live server by configuring an A record, reinforcing how DNS translates human-readable names to IP addresses.

🛠️ VS Code Setup
Set up a development environment with Python extensions, debugging tools, and terminal access to run and test scripts efficiently.

This journey reinforced the power of continuous learning and how AI can accelerate understanding in tech.

P.S. This post is part of the FREE DevOps Micro Internship Cohort run by Pravin Mishra. You can start your DevOps journey for free from his YouTube Playlist DevOps Micro Internship (#DMI) By Pravin Mishra (Cohort 1) - YouTube.

---

# Reflection – Week 0

### What did you find easy?

I found it easy to understand the basic networking concepts after breaking them down into smaller topics. Using ChatGPT as a learning assistant helped simplify technical terms like TCP/IP, packet switching, and DNS with real-world examples. I also enjoyed creating the application architecture diagrams because they helped me visualize how different application layers work together.

---

### What was difficult?

The most challenging part was connecting all the networking concepts into one complete picture, especially understanding how packets travel across the internet and how DNS, IP addresses, and HTTP/HTTPS interact during a user's request. It took some additional reading and practice before the entire process became clear.

---

### What will you improve next week?

I want to spend more time practicing hands-on activities alongside the theory. I plan to improve my understanding of Linux commands, networking fundamentals, and system architecture while documenting my learning more effectively. I also want to become more comfortable explaining technical concepts in simple terms, as this is an important skill for DevOps engineers.

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.


## 📌 Resources

- 🌐 **DMI Official Website:** https://pravinmishra.com/dmi  
- 🎓 **DevOps for Beginners (Udemy):** https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 **Ultimate Agentic AI DevOps with Clude Code** https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/?referralCode=448389767BC96284087B
- 🎓 **DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm** https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/?referralCode=1C5B734505D65A010FA3
- ▶️ **YouTube Playlist (DMI Cohort 3):** https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 **Pravin Mishra (LinkedIn):** https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 **CloudAdvisory (LinkedIn):** https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track*