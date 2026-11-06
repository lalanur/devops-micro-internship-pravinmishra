# Assignment 4 — Automate EpicBook Deployment with Dual Pipelines

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will automate the EpicBook infrastructure and application deployment on Microsoft Azure using two repositories and two Azure DevOps pipelines. Terraform will provision the infrastructure, and Ansible will configure the servers, connect EpicBook to Azure Database for MySQL, and deploy the application through Nginx.

---

# Task 0 — Verify Accounts, Tools, and Pipeline Capacity

## Goal

Confirm that the required accounts, tools, pipeline agent, SSH key pair, and Terraform remote-state location are ready.

No submission screenshot is required for this task.

---

# Task 1 — Prepare the Two Repositories

## Goal

Create separate Infrastructure and Application Repositories for the EpicBook deployment.

No submission screenshot is required for this task.

---

# Task 2 — Configure Azure DevOps Connections, Secure Files, and Secrets

## Goal

Configure controlled pipeline access to GitHub, Microsoft Azure, the virtual machines, and Azure Database for MySQL.

No submission screenshot is required for this task.

> Do not expose the Azure Client Secret, SSH private key, MySQL password, access token, subscription ID, or another sensitive value.

---

# Task 3 — Author the Terraform Infrastructure Configuration

## Goal

Define the complete EpicBook Azure infrastructure using Terraform and an Azure Storage remote backend.

No submission screenshot is required for this task.

---

# Task 4 — Author and Run the Infrastructure Pipeline

## Goal

Validate, plan, approve, and apply the Terraform configuration through the Infrastructure Pipeline.

## Evidence

### Screenshot 1 — Successful Infrastructure Pipeline

Add a screenshot of the Infrastructure Pipeline run showing:

* Successful `terraform apply` completion
* `app_public_ip`
* `backend_ansible_host`
* `backend_private_ip`
* `mysql_fqdn`

![screenshot 01](screenshots/task4-screenshot-01.PNG)

> Do not expose the MySQL password, Client Secret, Terraform state, SSH private key, or another sensitive value.

---

### Screenshot 2 — Provisioned Azure Resources

Add a screenshot of the Azure Portal Resource Group overview showing:

* Virtual Network and related networking resources
* Frontend VM
* Backend VM
* Azure Database for MySQL Flexible Server
* Related EpicBook resources

![screenshot 02](screenshots/task4-screenshot-02.PNG)

> Hide sensitive IDs, credentials, and database details.

---

# Task 5 — Complete the Manual Terraform-to-Ansible Handoff

## Goal

Transfer the required non-sensitive Terraform outputs to the Application Repository for use by Ansible.

No submission screenshot is required for this task.

---

# Task 6 — Author the Ansible Application Configuration

## Goal

Create idempotent Ansible automation that configures the frontend and backend VMs, prepares the database, configures Nginx, and deploys EpicBook.

No submission screenshot is required for this task.

---

# Task 7 — Author and Run the Application Pipeline

## Goal

Run the Application Pipeline to configure the VMs, deploy EpicBook, and verify the application environment.

## Evidence

### Screenshot 3 — Successful Application Pipeline

Add a screenshot of the Application Pipeline run summary showing all required stages or jobs succeeded.

![screenshot 03](screenshots/task4-screenshot-03.PNG)

---

### Screenshot 4 — Successful Ansible Play Recap

Add a screenshot of the Application Pipeline log showing:

* Ansible play recap
* Successful configuration or verification
* Zero failed hosts
* Zero unreachable hosts

![screenshot 04](screenshots/task4-screenshot-04.PNG)

> Do not expose the SSH private key, MySQL password, Client Secret, or complete database connection string.

---

# Task 8 — Verify the Complete EpicBook Workflow

## Goal

Verify that the frontend, backend, and Azure Database for MySQL work together correctly.

## Evidence

### Screenshot 5 — Running EpicBook Application

Add a browser screenshot showing:

* Running EpicBook application
* Frontend public IP address in the browser address bar
* Your Full Name
* Deployment date

The screenshot may show a product, cart, or successful order view.

![screenshot 05](screenshots/task4-screenshot-05.PNG)

![screenshot 05](screenshots/task4-screenshot-05ii.PNG)

> Do not expose credentials or sensitive information.

---

# Required URLs

## Frontend Application URL

[[http://4.154.73.19/]]

## Infrastructure Repository URL

[[https://dev.azure.com/lalanura5/epicbook-cicd/_git/infra-epicbook]]

## Application Repository URL

[[https://dev.azure.com/lalanura5/epicbook-cicd/_git/theepicbook]]

---

# Two-Repository Model

Write a short explanation of why separate Infrastructure and Application Repositories were used.

[Infrastructure changes live in `infra-epicbook` (Terraform + infra pipeline). Application configuration and EpicBook code live in `theepicbook` (Ansible + app pipeline). Separating the repos keeps infrastructure review stricter, limits which pipelines can touch Azure, and keeps application deploy history clear of Terraform state and cloud auth concerns.]

---

# Manual Terraform-to-Ansible Handoff

Write a short explanation of how the following non-sensitive Terraform outputs were transferred to the Application Repository:

* `app_public_ip`
* `backend_ansible_host`
* `backend_private_ip`
* `mysql_fqdn`

[After a successful infra apply, non-sensitive outputs (`app_public_ip`, `backend_ansible_host`, `backend_private_ip`, `mysql_fqdn`) are copied into the app repo inventory and `group_vars`. The MySQL password stays only in the secured Azure DevOps variable group. A commit to `theepicbook` main then runs the Ansible pipeline.]

---

# LinkedIn Requirement

## Evidence

### Screenshot 6 — LinkedIn Post

Add a screenshot of your LinkedIn post showing:

* Post text
* At least one image or link

![screenshot 06](screenshots/task4-screenshot-06.PNG)

## LinkedIn Post URL

[https://www.linkedin.com/posts/zahra-u-nura_dmibypravinmishra-devops-microsoftazure-ugcPost-7524483876090728448-lTVA/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABhheJ4Bw5LI3hMBUfCD5MZiGRXdKYKjr0U]

Your post must include:

* What you automated
* Why separate Infrastructure and Application Repositories were used
* A brief explanation of the Terraform and Ansible pipelines
* How Azure credentials, the SSH key, and database secrets were protected
* One challenge you encountered
* How you solved the challenge
* Relevant technologies and skills

> Do not expose credentials, SSH keys, database passwords, subscription details, or other sensitive information.

---

# Submission Instructions

* Complete all tasks in sequence.
* Include your Full Name.
* Include a short explanation of the two-repository model.
* Include a short explanation of the manual Terraform-to-Ansible handoff.
* Include the Infrastructure Repository URL.
* Include the Application Repository URL.
* Include the final EpicBook application URL.
* Include Screenshots 1–6.
* Include the public LinkedIn post URL.
* Confirm that all screenshots are readable.
* Do not include Terraform state.
* Do not expose the Azure Client Secret, MySQL password, SSH private key, access token, complete connection string, subscription ID, tenant ID, account ID, or another sensitive value.
* Follow the Assignment Submission Guidelines.

---

# Completion Checklist

* [ ] Two separate repositories were created
* [ ] The Infrastructure Repository contains Terraform and its pipeline
* [ ] The Application Repository contains EpicBook, Ansible, and its pipeline
* [ ] Your Full Name and deployment date are visible in EpicBook
* [ ] Both pipelines use the intended `main` branch
* [ ] The Azure Resource Manager Service Connection works
* [ ] The Azure Client Secret is not stored in Git or YAML
* [ ] Terraform uses an Azure Storage remote backend
* [ ] Terraform state was not published or committed
* [ ] Separate frontend, backend, and database subnets were created
* [ ] The frontend VM accepts public HTTP traffic on port 80
* [ ] SSH access is restricted
* [ ] The backend application port is not publicly accessible
* [ ] Azure Database for MySQL uses private access
* [ ] The Infrastructure Pipeline validates, plans, applies, and displays non-sensitive outputs
* [ ] The reviewed Terraform plan was used during Apply
* [ ] Approval or manual validation occurred before Apply
* [ ] `app_public_ip` is available
* [ ] `backend_ansible_host` is available
* [ ] `backend_private_ip` is available
* [ ] `mysql_fqdn` is available
* [ ] Only non-sensitive Terraform outputs were transferred to the Application Repository
* [ ] The SSH private key is stored in Azure DevOps Secure Files
* [ ] The SSH private key was not committed or published
* [ ] The MySQL password is stored as a secret pipeline variable
* [ ] Ansible reaches both frontend and backend VMs
* [ ] Ansible completes with zero failed and zero unreachable hosts
* [ ] Nginx proxies requests to the backend private IP
* [ ] EpicBook runs as a persistent service
* [ ] The database schema and seed data are available
* [ ] The application displays database-backed products
* [ ] Cart or checkout actions are recorded in MySQL
* [ ] The final application displays your Full Name and deployment date
* [ ] Screenshots 1–6 are included and readable
* [ ] The Infrastructure Repository URL is included
* [ ] The Application Repository URL is included
* [ ] The final EpicBook application URL is included
* [ ] The LinkedIn post is published
* [ ] The LinkedIn post URL is included
* [ ] No secret or sensitive identifier is exposed

---

*This submission is part of the DevOps Micro Internship (DMI) — Agentic AI Track.*
