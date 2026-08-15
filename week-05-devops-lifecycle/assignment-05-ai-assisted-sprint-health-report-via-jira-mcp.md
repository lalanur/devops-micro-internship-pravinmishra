# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

![screenshot 01](screenshots/task5-screenshot-01.PNG)

![screenshot 01](screenshots/task5-screenshot-01ii.PNG)

### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

The token proves that the MCP server is authorized to access the account, while the site URL tells it which instance to connect to and the account email identifies the user/account making the request. Together, these details allow the MCP server to connect to the correct Jira environment and authenticate the correct account securely.

---

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

![screenshot 02](screenshots/task5-screenshot-02.PNG)

### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

The structure stays the same in both configurations: each defines an `mcpServers` object containing a server name (`github` or `jira`), a `command`, `args`, and `env` section. The only major difference is how the server is launched—GitHub uses **`npx`** for a Node.js package, while Jira uses `uvx` for a Python package.

Claude Code does not need to know which programming language the MCP server uses because it communicates with the server through the MCP protocol. As long as the server follows that protocol and can be started using the configured command, Claude interacts with it in the same standardized way.


---

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

![screenshot 03](screenshots/task5-screenshot-03.PNG)

### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

JIRA_API_TOKEN should be stored in settings.local.json because it is a secret credential and should remain local to your environment. Putting it in .mcp.json could expose the token if that file is committed to Git or shared with the team. Keeping it in the local settings file separates configuration that can be shared from credentials that must remain private.

---

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

![screenshot 04](screenshots/task5-screenshot-04.PNG)

---

# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

![screenshot 05](screenshots/task5-screenshot-05.PNG)

### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

I confirmed it by checking the actual Jira board in the browser and comparing the issues, statuses, and sprint information with what Claude reported. This verified that Claude was retrieving live Jira data through the MCP server rather than generating an assumption.

---

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

![screenshot 06](screenshots/task5-screenshot-06.PNG)

#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

![screenshot 07](screenshots/task5-screenshot-07.PNG)

### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

The skill is restricted to read-only Jira tools, such as tools for searching and retrieving issues, boards, sprints, and project information. It deliberately excludes mutating actions such as create issue, update issue, transition issue, and add comment, so Claude can inspect the board without changing it.

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

The Scrum Master needs to maintain the accuracy and integrity of the Scrum process without taking ownership of the team's work. Keeping the skill read-only allows me to use AI for visibility and analysis while ensuring that changes to Jira remain under human control.

---

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

![screenshot 08](screenshots/task5-screenshot-08.PNG)

### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

Gather: Claude used the Jira MCP tools to retrieve the actual board, sprint, issue, and status information.
Analyze: Claude reviewed the Jira data and summarized the team's progress and Scrum-related information.
Human Act: I manually made the required changes in the Jira browser. This must remain human because changing issues or sprint information affects the team's official project record and should require deliberate approval.
Verify: I checked the Jira board again in the browser to confirm that the changes were correctly reflected and that the board matched the expected state.

---

# Submission Instructions

Complete all tasks in sequence.

Your submission must include:
- All 8 required screenshots
- All the required notes

---

# Completion Checklist

- [ ] Task 1: Jira API token created, value never screenshotted (Screenshot 1)
- [ ] Task 2: `.mcp.json` has the Jira server block (Screenshot 2)
- [ ] Task 3: Credentials stored in `settings.local.json`, token blurred, file gitignored (Screenshot 3)
- [ ] Task 4: `/mcp` shows the Jira server connected (Screenshot 4)
- [ ] Task 5: Live query returned real sprint data, verified against the browser (Screenshot 5)
- [ ] Task 6: `/sprint-health` skill created with correct read-only `allowed-tools`, and produced a full report (Screenshots 6–7)
- [ ] Task 7: A manual board change was reflected in a second `/sprint-health` run (Screenshot 8)
- [ ] Skill never created, edited, transitioned, or commented on any issue
- [ ] Reflection answered (Notes)
- [ ] No API token value exposed

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
