---
name: jira-daily-report
description: Generates a daily work report by scanning Jira tasks from a given Jira link within a specified date range (defaults to today).
---

# Daily Report Skill

This skill automates the process of fetching, analyzing, and formatting your Jira tasks into a professional daily/period report.

## Trigger Command
To trigger this skill, the user will type:
`/jira-daily-report <Jira_Link> [Start_Date] [End_Date]`

---

## Step-by-Step Execution Guide for Claude

### 1. Parse Inputs
When this command is run, extract the parameters:
*   **Jira Link (Required):** The base URL, project board, or specific epic/filter link.
*   **Start Date (Optional):** If not provided, default to **today's date** (determine today's date using system time).
*   **End Date (Optional):** If not provided, default to **today's date**.
*   *Note:* Accept dates in formats like `YYYY-MM-DD`, or relative terms like `yesterday` or `today` (and convert them to actual dates).

### 2. Access Jira
Since you have access to the company's Jira system:
*   Determine the best method to fetch data. Look for local command-line tools (e.g., `jira` CLI), environment variables (like `JIRA_API_TOKEN`, `JIRA_USER`), or use standard `curl` commands to query the Jira REST API.
*   Construct a JQL (Jira Query Language) query to find tickets that meet the following criteria:
    *   Associated with the provided **Jira Link** (e.g., matches the Project Key, Board, or Epic parsed from the URL).
    *   Assigned to the current user (if applicable) or updated/resolved/created between the **Start Date** and **End Date**.
    *   *Draft JQL base:* `assignee = currentUser() AND updated >= "Start_Date 00:00" AND updated <= "End_Date 23:59"`

### 3. Retrieve and Analyze Task Details
Fetch the following details for each ticket found:
*   Key (e.g., PROJ-123) and Summary (Title).
*   Current Status (e.g., To Do, In Progress, Under Review, Done).
*   Latest comment or update description during the selected date range.

### 4. Generate the Daily Report
Draft a clean, professional report in markdown using the template below.

---

## Output Template

# Daily Work Report
**Period:** [Start Date] to [End Date]
**Target Project/Board:** [Jira Link]

### 🚀 Completed Tasks
*   **[PROJ-123] Ticket Title**
    *   *Status:* Done
    *   *Summary of work:* [1-sentence summary of what was accomplished]

### 🔨 In Progress / Active Tasks
*   **[PROJ-124] Ticket Title**
    *   *Status:* [e.g., In Progress / In Code Review]
    *   *Next Steps:* [What needs to be done next]

### ⚠️ Blockers / Impediments (If any)
*   *None* (or list tickets that are blocked and why)