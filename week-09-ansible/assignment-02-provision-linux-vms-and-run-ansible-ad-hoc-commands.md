# Assignment 02 — Provision Linux VMs with Terraform and Run Ansible Ad-Hoc Commands

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will use Terraform to provision three or four Ubuntu Linux Virtual Machines on either Microsoft Azure or Amazon Web Services.

You will configure SSH key-based authentication, organize the servers using a custom Ansible inventory, and run Ansible ad-hoc commands across individual hosts and inventory groups.

---

# Task 1 — Create the Multi-Host Lab Structure

## Goal

Create a separate project directory for the multi-host lab and prepare the Terraform, Ansible, and documentation files.

This project will use the Git repository and Ansible controller prepared in Assignment 01.

### Evidence

#### Screenshot 1 — Terminal showing the complete `ansible-adhoc-lab` project structure

![screenshot 01](screenshots/task2-screenshot-01.PNG)

---

#### Screenshot 2 — Terminal showing `git status --short` with the new project files and updated `.gitignore`

![screenshot 02](screenshots/task2-screenshot-02.PNG)

---

### Notes

Created the ansible-adhoc-lab project within my existing Ansible workspace. Organized separate directories for Terraform and Ansible files and updated .gitignore to prevent sensitive Terraform state files from being committed to Git.

---

# Task 2 — Create the Terraform Configuration

## Goal

Create the Terraform configuration required to provision three or four Ubuntu Linux VMs on your selected cloud platform.

Complete only one option:

- Option A — Microsoft Azure
- Option B — Amazon Web Services

Do not configure both providers for this assignment.

### Evidence

#### Screenshot 3 — Terraform configuration showing the three or four server roles and the `for_each` or `count` implementation

![screenshot 03](screenshots/task2-screenshot-03.PNG)

---

#### Screenshot 4 — Terraform configuration showing SSH restricted to the controller IP and HTTP allowed only for web hosts

![screenshot 04](screenshots/task2-screenshot-04.PNG)

---

#### Screenshot 5 — Terraform output configuration showing how public IP addresses are associated with the server roles

![screenshot 05](screenshots/task2-screenshot-05.PNG)

---

### Notes

Configured Terraform using the AzureRM provider to define three Ubuntu virtual machines (web1, app1, and db1). Used for_each for automated resource creation, configured networking and SSH security rules, and defined outputs for public IP addresses.

---

# Task 3 — Provision the Infrastructure with Terraform

## Goal

Initialize and validate the Terraform configuration, review the execution plan, provision the selected three or four VMs, and retrieve their public IP addresses.

### Evidence

#### Screenshot 6 — Final `terraform apply` output showing `Apply complete`

![screenshot 06](screenshots/task2-screenshot-06.PNG)

---

#### Screenshot 7 — `terraform output public_ips` showing the role-to-IP mapping for all three or four VMs

![screenshot 07](screenshots/task2-screenshot-07.PNG)

---

#### Screenshot 8 — Azure Portal or AWS Management Console showing all three or four VMs in the `Running` state, with their role-based names visible

![screenshot 08](screenshots/task2-screenshot-08.PNG)

---

### Notes

Used Terraform to initialize, validate, plan, and deploy the Azure infrastructure. Configured networking resources and public IP addresses for the three virtual machines and used Terraform outputs to identify each server.

---

# Task 4 — Verify SSH Key-Based Access

## Goal

Verify that each managed VM can be accessed from the Ansible controller using SSH key-based authentication.

### Evidence

#### Screenshot 9 — Terminal showing successful SSH hostname output from all VMs

![screenshot 09](screenshots/task2-screenshot-09.PNG)

---

### Notes

Configured SSH key-based authentication to access the Azure virtual machines securely. Tested SSH connectivity from the Ubuntu WSL controller and verified the servers using hostname commands.

---

# Task 5 — Create the Custom Ansible Inventory

## Goal

Create an Ansible inventory file that groups the managed VMs by role.

The inventory allows Ansible to run commands against all servers, or only specific groups such as `web`, `app`, or `db`.

### Evidence

#### Screenshot 10 — `inventory.ini` showing the `web`, `app`, and `db` groups

![screenshot 10](screenshots/task2-screenshot-10.PNG)

---

#### Screenshot 11 — Output of `ansible-inventory -i inventory.ini --graph`

![screenshot 11](screenshots/task2-screenshot-11.PNG)

---

### Notes

Created an inventory.ini file containing the three Azure virtual machines, organized into web, app, and db groups. Configured the SSH username and private-key path, then validated the inventory structure using ansible-inventory --graph.

---

# Task 6 — Run Ansible Ad-Hoc Commands

## Goal

Run Ansible ad-hoc commands from the controller to verify connectivity, check server information, and manage packages and services across inventory groups.

This task proves that the inventory is working and that Ansible can control multiple managed VMs without writing a playbook.

### Evidence

#### Screenshot 12 — Output of `ansible all -i inventory.ini -m ping`

![screenshot 12](screenshots/task2-screenshot-12.PNG)

---

#### Screenshot 13 — Output of `ansible all -i inventory.ini -m command -a "uptime"`

![screenshot 13](screenshots/task2-screenshot-13.PNG)

---

#### Screenshot 14 — Output of `ansible web -i inventory.ini -m apt -a "name=nginx state=present update_cache=yes" --become`

![screenshot 14](screenshots/task2-screenshot-14.PNG)

---

#### Screenshot 15 — Output of `ansible web -i inventory.ini -m service -a "name=nginx state=started enabled=yes" --become`

![screenshot 16](screenshots/task2-screenshot-16.PNG)

---

#### Screenshot 16 — Output of `ansible all -i inventory.ini -m apt -a "name=htop state=present update_cache=yes" --become`

![screenshot 16](screenshots/task2-screenshot-16.PNG)

---

#### Screenshot 17 — Output of `ansible web -i inventory.ini -m command -a "systemctl is-active nginx"`

![screenshot 17](screenshots/task2-screenshot-17.PNG)

---

### Notes

Successfully verified Ansible connectivity to all three Azure VMs using the ping module. Used Ansible ad-hoc commands to check server uptime, manage Nginx on the web server, install htop, and perform system administration tasks across inventory groups.

---

# LinkedIn Post Required

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/zahra-u-nura_aws-agenticai-claudecode-ugcPost-7518022638317846528-tfvV/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABhheJ4Bw5LI3hMBUfCD5MZiGRXdKYKjr0U`

---

#### Screenshot — Published LinkedIn post

![screenshot 18](screenshots/task2-screenshot-18.PNG)

---

# Assignment Questions

Answer the following in your own words:

**1. What is the purpose of an Ansible inventory file?**

An Ansible inventory file lists the servers Ansible manages, including their IP addresses, connection details, and groups. It allows Ansible to target specific servers or multiple hosts at once.

---

**2. What is the difference between the `web`, `app`, and `db` groups in your inventory?**

The web group contains web servers, the app group contains application servers, and the db group contains database servers. These groups allow me to run commands on specific servers based on their roles.

---

**3. What does the Ansible `ping` module verify?**

The Ansible ping module verifies that Ansible can connect to a managed server through SSH, authenticate successfully, and execute Python modules. It does not perform a traditional network ping.

---

**4. Why do package installation commands require `--become`?**

Package installation requires administrator privileges. The --become option allows Ansible to execute commands with elevated privileges, usually through sudo.

---

**5. When would you use an ad-hoc command instead of a playbook?**

I would use an ad-hoc command for quick, one-time tasks such as checking server uptime, installing a package, or restarting a service. Playbooks are better for repeatable automation involving multiple tasks.

---

**6. What is one challenge you faced while setting up SSH or inventory, and how did you fix it?**

One challenge was ensuring Ansible could connect to all three Azure VMs using SSH. I configured the correct public IP addresses, SSH username, and private-key path in the inventory. I then verified connectivity using the Ansible ping module, which returned SUCCESS and pong for all three servers.

---

# Required Files

Confirm that the following files are included in your assignment workspace:

- [ ] `ansible-adhoc-lab/README.md`
- [ ] `ansible-adhoc-lab/terraform/providers.tf`
- [ ] `ansible-adhoc-lab/terraform/main.tf`
- [ ] `ansible-adhoc-lab/terraform/variables.tf`
- [ ] `ansible-adhoc-lab/terraform/outputs.tf`
- [ ] `ansible-adhoc-lab/ansible/inventory.ini`
- [ ] Updated `.gitignore`

---

# Submission Instructions

- Add all required screenshots from the tasks.
- Full Name must be visible in required screenshots.
- Mention whether you used Azure or AWS.
- Mention whether you used the three-VM option or four-VM option.
- Add the public IP addresses of the VMs, redacted if preferred.
- Add your `inventory.ini` proof.
- Add a short explanation of what you learned.
- Answer all assignment questions clearly in your own words.
- Add your LinkedIn post URL.
- Do not expose SSH private keys, Terraform state files, cloud credentials, passwords, access keys, secret keys, account IDs, or subscription IDs.

---

# Completion Checklist

- [ ] Task 1: `ansible-adhoc-lab` project structure created
- [ ] Task 1: `.gitignore` updated for Terraform files
- [ ] Task 2: Terraform configuration created
- [ ] Task 2: Server roles defined for either three or four VMs
- [ ] Task 2: `count` or `for_each` used
- [ ] Task 2: SSH restricted to the controller public IP
- [ ] Task 2: HTTP allowed only for web hosts
- [ ] Task 2: Terraform output maps roles to public IPs
- [ ] Task 3: Terraform initialized successfully
- [ ] Task 3: Terraform configuration validated
- [ ] Task 3: Terraform apply completed successfully
- [ ] Task 3: All selected VMs are running
- [ ] Task 4: SSH key-based access works for every VM
- [ ] Task 5: `inventory.ini` contains `web`, `app`, and `db` groups
- [ ] Task 5: `ansible-inventory -i inventory.ini --graph` shows the correct groups
- [ ] Task 6: `ansible all -i inventory.ini -m ping` returns `SUCCESS`
- [ ] Task 6: Ad-hoc commands run successfully
- [ ] Task 6: `--become` was used for package and service tasks
- [ ] Task 6: Nginx is active on the `web` group
- [ ] Screenshots 1–17 are included
- [ ] Assignment questions are answered
- [ ] LinkedIn post published
- [ ] LinkedIn post URL added
- [ ] No sensitive information is exposed

---

## About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra and The CloudAdvisory, focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## Resources

- DMI Official Website: [https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme](https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme)
- University: [https://university.pravinmishra.com?utm_source=github&utm_medium=readme](https://university.pravinmishra.com?utm_source=github&utm_medium=readme)
- Discord Community: [https://discord.pravinmishra.com?utm_source=github&utm_medium=readme](https://discord.pravinmishra.com?utm_source=github&utm_medium=readme)
- Blog: [https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme](https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme)
- YouTube Playlist: [https://www.youtube.com/playlist?list=PLFeSNDtI4Cho](https://www.youtube.com/playlist?list=PLFeSNDtI4Cho)
- Pravin Mishra LinkedIn: [https://www.linkedin.com/in/pravin-mishra-aws-trainer/](https://www.linkedin.com/in/pravin-mishra-aws-trainer/)
- CloudAdvisory LinkedIn: [https://www.linkedin.com/company/thecloudadvisory/](https://www.linkedin.com/company/thecloudadvisory/)

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*