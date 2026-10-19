# Assignment 6 — AI-Assisted Ansible Change Risk Review

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will build an AI-assisted Ansible risk-review workflow using `ansible-playbook --check --diff`, Bash scripting, and Claude Code.

You will review possible server changes before applying them, classify risky tasks, and keep the final apply decision under human control.

---

# Task 1 — Confirm EpicBook Connectivity and Create the Workspace

## Goal

Confirm that your previous EpicBook Ansible project is working before creating the risk-review automation.

### Evidence

#### Screenshot 1 — Output of `ansible web -i inventory.ini -m ping`

![screenshot 01](screenshots/task6-screenshot-01.PNG)

---

#### Screenshot 2 — Output of `ansible-playbook -i inventory.ini site.yml --syntax-check`

![screenshot 02](screenshots/task6-screenshot-02.PNG)

---

#### Screenshot 3 — Output of `pwd` and `find . -maxdepth 4 -type d | sort`

![screenshot 03](screenshots/task6-screenshot-03.PNG)

---

### Notes

Answer the following in your own words:

**1. What proves that Ansible can reach your EpicBook VM?**

The successful Ansible ping showing SUCCESS and pong confirms that Ansible can connect to the VM using SSH.

---

**2. Why should you confirm playbook syntax before building a risk-review script?**

To ensure the playbook is valid and prevent existing YAML or Ansible errors from interfering with the risk-review process.

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Create a `CLAUDE.md` file that tells Claude Code how this project must behave.

### Evidence

#### Screenshot 4 — `CLAUDE.md` open in VS Code or terminal showing the safety rules

![screenshot 04](screenshots/task6-screenshot-04.PNG)

---

### Notes

Answer the following in your own words:

**1. Why should Claude Code have project-specific safety rules?**

To ensure it follows the project's requirements and avoids making unauthorized changes to servers or configuration files.

---

**2. Why should the human run the real Ansible playbook manually?**

Because infrastructure changes can affect live services, and a human should review the risks before approving deployment.

---

**3. Which rule prevents Claude Code from applying changes automatically?**

The rule: "Never apply, converge, or fix the playbook automatically.

---

# Task 3 — Ask Claude Code to Plan the Risk Review

## Goal

Use Claude Code to produce a read-only plan before writing the Bash script.

### Evidence

#### Screenshot 5 — Claude Code showing the four-category risk-classification plan

![screenshot 05](screenshots/task6-screenshot-05.PNG)

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

Reviewing the existing Ansible playbook and planning how to collect dry-run evidence using --check --diff.

---

**2. Which part represents the Analyze phase?**

Claude Code identifying the four risk categories, their task-name patterns, and their possible impact.

---

**3. How did you verify Claude Code did not create or edit files?**

I compared the workspace files before and after the Claude Code session and checked that no project files were unexpectedly changed.

---

# Task 4 — Build the Ansible Risk Review Script

## Goal

Create a Bash script that runs an Ansible dry run and classifies risky changes.

### Evidence

#### Screenshot 6 — Top section of `ansible-check-review.sh` showing `full_name`, `playbook_path`, `inventory_path`, and the `checks` array

![screenshot 06](screenshots/task6-screenshot-06.PNG)

---

#### Screenshot 7 — Middle section showing `extract_changed_tasks` and `check_tasks_matching_pattern`

![screenshot 07](screenshots/task6-screenshot-07.PNG)

---

#### Screenshot 8 — Bottom section showing the loop, summary, and exit behavior

![screenshot 08](screenshots/task6-screenshot-08.PNG)

---

#### Screenshot 9 — Output of `bash -n ansible-check-review.sh` and `ls -l ansible-check-review.sh`

![screenshot 09](screenshots/task6-screenshot-09.PNG)

---

### Notes

Answer the following in your own words:

**1. What is stored in the `changed_tasks` array?**

It stores the names of Ansible tasks that reported changes during the dry run.

---

**2. Which function finds changed tasks from the Ansible output?**

The extract_changed_tasks() function uses awk and sed to identify changed tasks.

---

**3. Why does the script use `--check --diff`?**

To preview configuration changes and show differences without intentionally applying them.

---

**4. Why does the script use different exit codes for healthy, warning, and failed results?**

To clearly distinguish successful checks, changes requiring review, and potentially risky or failed checks.

---

# Task 5 — Run the Baseline Dry-Run Review

## Goal

Run the script against your current EpicBook playbook and confirm the baseline risk status.

### Evidence

#### Screenshot 10 — Output of `./ansible-check-review.sh`

![screenshot 10](screenshots/task6-screenshot-10.PNG)

---

#### Screenshot 11 — Output of `echo "Captured Exit Code: $script_exit_code"` and `cat reports/ansible-risk-report.txt`

![screenshot 11](screenshots/task6-screenshot-11.PNG)

---

### Notes

Answer the following in your own words:

**1. What was the overall status of your baseline run?**

The baseline review reported HEALTHY.

---

**2. Did any tasks report `changed`?**

No, the script did not detect any changed tasks.

---

**3. Were any changed tasks flagged as risky?**

No, no changed tasks were flagged as risky.

---

**4. What does the script exit code mean?**

The exit code indicates the review result: 0 means HEALTHY, 1 means WARN, and 2 means FAIL.

---

# Task 6 — Create and Run the Claude Code Skill

## Goal

Turn the Bash script into a reusable Claude Code skill called `/ansible-risk-review`.

### Evidence

#### Screenshot 12 — `SKILL.md` showing the frontmatter, allowed tools, and safety rules

![screenshot 12](screenshots/task6-screenshot-12.PNG)

---

#### Screenshot 13 — Claude Code output after running `/ansible-risk-review`

![screenshot 13](screenshots/task6-screenshot-13.PNG)

---

### Notes

Answer the following in your own words:

**1. Why does this skill allow `Bash`, `Read`, and `Grep`?**

Bash executes the dry-run script, while Read and Grep allow Claude Code to inspect the generated reports.

---

**2. Why does this skill not allow file editing?**

To prevent Claude Code from making unauthorized changes to the playbook, configuration files, or infrastructure..

---

**3. What part is handled by Bash?**

Bash runs the Ansible dry run, detects changed tasks, classifies risks, and generates the report.

---

**4. What part is handled by Claude Code?**

Claude Code analyzes the report, explains the risks, and recommends whether human review is needed.

---

**5. Why is this better than asking Claude Code if the playbook is safe without giving it evidence?**

Because the recommendation is based on actual Ansible dry-run output rather than assumptions.

---

# Task 7 — Introduce a Controlled Risky Change and Let the Skill Catch It

## Goal

Add a small controlled risky change in your lab playbook and confirm the script and Claude Code catch it before applying.

### Evidence

#### Screenshot 14 — The added risky task inside the role file

![screenshot 14](screenshots/task6-screenshot-14.PNG)

---

#### Screenshot 15 — Output of `./ansible-check-review.sh`

![screenshot 15](screenshots/task6-screenshot-15.PNG)

---

#### Screenshot 16 — Claude Code `/ansible-risk-review` output showing the risky finding

![screenshot 16](screenshots/task6-screenshot-16.PNG)

---

#### Screenshot 17 — Output of `cat reports/risky-change-report.txt`

![screenshot 17](screenshots/task6-screenshot-17.PNG)

---

### Notes

Answer the following in your own words:

**1. Which risk category did the added task fall into?**

The task was classified under the file-removal risk category.

---

**2. What evidence proves the task would change something?**

The Ansible dry run reported the removal task as changed, and the risk-review report identified it as a pending removal.

---

**3. Did Claude Code apply the playbook?**

No. Claude Code only ran the dry-run review and analyzed the findings.

---

**4. Why is it important that Claude Code only analyzed the risk?**

It ensures that a human reviews and approves changes before they affect the server.

---

**5. Which phase of the Agentic Loop is represented by the Bash report?**

The Gather phase, because the Bash script collects dry-run evidence for risk analysis.

---

# Task 8 — Apply as the Human, Verify, and Write the Change Summary

## Goal

Review the risky-change report, apply the playbook manually as the human operator, and verify the result.

### Evidence

#### Screenshot 18 — Output of the real playbook run showing the final recap with `failed=0`

![screenshot 18](screenshots/task6-screenshot-18.PNG)

---

#### Screenshot 19 — Output of `ansible web -i inventory.ini -m ping`

![screenshot 19](screenshots/task6-screenshot-19.PNG)

---

#### Screenshot 20 — Second `/ansible-risk-review` output after applying the change

![screenshot 2](screenshots/task6-screenshot-2.PNG)

---

#### Screenshot 21 — Output of `ls -lah reports`

![screenshot 21](screenshots/task6-screenshot-21.PNG)

---

#### Screenshot 22 — `change-summary.md` showing all required sections and your Full Name

![screenshot 22](screenshots/task6-screenshot-22.PNG)

---

### Notes

Answer the following in your own words:

**1. What command did you run to apply the change for real?**

ansible-playbook -i inventory.ini site.yml.

---

**2. Who made the final decision to apply the playbook?**

I made the final decision after reviewing the risk report.

---

**3. What evidence proves the VM is still reachable?**

The successful Ansible ping response showing SUCCESS and pong.

---

**4. Why should the risk review be run again after applying?**

To verify that the intended change is no longer pending and identify any remaining configuration differences.

---

**5. What could go wrong if an AI agent applied Ansible changes automatically?**

It could accidentally delete files, restart critical services, change permissions, or disrupt production systems without human approval.

---

# LinkedIn Post Required

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/zahra-u-nura_dmibypravinmishra-devops-ansible-share-7518030342944030720-0kkR/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABhheJ4Bw5LI3hMBUfCD5MZiGRXdKYKjr0U`

---

#### Screenshot — Published LinkedIn post

![screenshot 23](screenshots/task6-screenshot-23.PNG)

---

# Required Files

Confirm that the following files are included in your GitHub repository or assignment folder:

- [ ] `CLAUDE.md`
- [ ] `ansible-check-review.sh`
- [ ] `.claude/skills/ansible-risk-review/SKILL.md`
- [ ] `reports/risky-change-report.txt`
- [ ] `reports/post-apply-report.txt`
- [ ] `change-summary.md`

---

# Submission Instructions

- Add all required screenshots in your submission.
- Full Name must be visible in required screenshots and reports.
- All required notes must be answered clearly.
- Do not expose SSH private keys, passwords, cloud credentials, database credentials, or secret environment variables.
- Add your GitHub repository or folder URL inside this document.

---

# Completion Checklist

- [ ] Task 1: EpicBook connectivity confirmed and workspace created
- [ ] Task 2: `CLAUDE.md` created with safety rules
- [ ] Task 3: Claude Code produced a read-only risk-review plan
- [ ] Task 4: `ansible-check-review.sh` created and syntax checked
- [ ] Task 5: Baseline dry-run review completed
- [ ] Task 6: Claude Code `/ansible-risk-review` skill created and tested
- [ ] Task 7: Controlled risky change introduced and detected
- [ ] Task 8: Human applied the change and verified the result
- [ ] Risky-change report saved
- [ ] Post-apply report saved
- [ ] Change summary completed
- [ ] All screenshots added
- [ ] All notes answered
- [ ] LinkedIn post published
- [ ] LinkedIn post URL added
- [ ] No sensitive information exposed

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