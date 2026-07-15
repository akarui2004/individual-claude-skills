# Installation Guide: Jira Daily Report Skill

This guide covers how to install the **jira-daily-report** skill into Claude AI (Web) or Claude Code (VSCode, CLI, or other environments).

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation for Claude Web](#installation-for-claude-web)
- [Installation for Claude Code](#installation-for-claude-code)
- [Verification & Testing](#verification--testing)
- [Troubleshooting](#troubleshooting)

---

## Prerequisites

Before installing the skill, ensure you have:

### 1. **Jira Credentials**
   - Jira API token or password for your Jira instance
   - Your Jira username/email
   - Your Jira instance URL (e.g., `https://your-company.atlassian.net`)

### 2. **Environment Variables (Optional but Recommended)**
   Set these for seamless Jira access:
   ```bash
   export JIRA_API_TOKEN="your_jira_api_token"
   export JIRA_USER="your_email@company.com"
   export JIRA_DOMAIN="your-company.atlassian.net"
   ```

### 3. **Jira CLI (Optional)**
   For enhanced functionality, install the Jira CLI:
   ```bash
   # macOS
   brew install jira-cli

   # Linux
   curl -L https://github.com/go-jira/jira/releases/download/v1.0.27/jira-linux-amd64 -o /usr/local/bin/jira
   chmod +x /usr/local/bin/jira
   ```

---

## Installation for Claude Web

### Step 1: Prepare the Skill Package

1. Navigate to the skill directory:
   ```bash
   cd /path/to/MyAISkills/claude/SKILLs/jira-daily-report
   ```

2. Verify the `SKILL.md` file exists and contains the proper metadata header:
   ```markdown
   ---
   name: jira-daily-report
   description: Generates a daily work report by scanning Jira tasks...
   ---
   ```

3. Create a compressed package:
   ```bash
   # Create a folder with the skill
   cd ..
   mkdir -p jira-daily-report-package
   cp -r jira-daily-report/* jira-daily-report-package/

   # Ensure the main file is named SKILL.md
   # (it should already be)

   # Create a ZIP archive
   zip -r jira-daily-report.zip jira-daily-report-package/
   ```

### Step 2: Upload to Claude.ai

1. Go to **[claude.ai](https://claude.ai)** and log in

2. Enable code execution (required for Jira API calls):
   - Click **Settings** (bottom left)
   - Select **Capabilities**
   - Toggle on **"Code execution"** and **"File creation"**

3. Access the Skills menu:
   - Click **Customize** in the left sidebar
   - Select the **Skills** tab

4. Upload the skill:
   - Click **"+ Create skill"** or **"+"** button
   - Select **"Upload a skill"**
   - Choose the `jira-daily-report.zip` file you created
   - Click **Upload**

5. Enable the skill:
   - Once uploaded, toggle the switch to **Enable**
   - The skill is now active!

### Step 3: Verify Installation

Test the skill with a sample command:
```
/jira-daily-report https://your-company.atlassian.net/jira/board-key
```

The skill should fetch and display your Jira tasks for today.

---

## Installation for Claude Code

### Option A: Global Installation (All Projects)

Install the skill globally so it's available in every project:

1. **Create the skill directory:**
   ```bash
   mkdir -p ~/.claude/skills/jira-daily-report
   ```

2. **Copy the SKILL.md file:**
   ```bash
   cp /path/to/MyAISkills/claude/SKILLs/jira-daily-report/SKILL.md \
      ~/.claude/skills/jira-daily-report/SKILL.md
   ```

3. **Verify the file exists:**
   ```bash
   ls -la ~/.claude/skills/jira-daily-report/
   ```

4. **Restart Claude Code** (VSCode, CLI, or other):
   - Close and reopen your editor
   - The skill should now be available

### Option B: Project-Specific Installation

Install the skill for a single project only:

1. **Create the skill directory in your project:**
   ```bash
   mkdir -p .claude/skills/jira-daily-report
   ```

2. **Copy the SKILL.md file:**
   ```bash
   cp /path/to/MyAISkills/claude/SKILLs/jira-daily-report/SKILL.md \
      .claude/skills/jira-daily-report/SKILL.md
   ```

3. **Verify the file exists:**
   ```bash
   ls -la .claude/skills/jira-daily-report/
   ```

4. **Restart Claude Code** and open this project
   - The skill will now be available within this project only

### Step 3: Configure Jira Credentials (Claude Code)

For Claude Code to access your Jira instance, set up credentials:

#### Option 1: Use Environment Variables
```bash
export JIRA_API_TOKEN="your_api_token"
export JIRA_USER="your_email@company.com"
```

#### Option 2: Use Jira CLI Configuration
```bash
# Configure the Jira CLI
jira configure -H https://your-company.atlassian.net -u your_email@company.com -p your_api_token
```

#### Option 3: Create a `.env` File (Project-Specific)
```bash
# In your project root
echo "JIRA_API_TOKEN=your_api_token" > .env
echo "JIRA_USER=your_email@company.com" >> .env
echo "JIRA_DOMAIN=your-company.atlassian.net" >> .env
```

---

## Verification & Testing

### Test the Skill Installation

1. **In Claude Web:**
   ```
   /jira-daily-report https://your-company.atlassian.net/jira/your-board
   ```

2. **In Claude Code (VSCode):**
   - Type `/jira-daily-report` in the Claude chat panel
   - The command should auto-complete if properly installed

3. **Test with Date Range:**
   ```
   /jira-daily-report https://your-company.atlassian.net/jira/your-board 2026-07-10 2026-07-15
   ```

4. **Test with Relative Dates:**
   ```
   /jira-daily-report https://your-company.atlassian.net/jira/your-board yesterday
   ```

### Expected Output

You should see a markdown report containing:
- ✅ **Completed Tasks** section
- 🔨 **In Progress / Active Tasks** section
- ⚠️ **Blockers / Impediments** section (if any)

---

## Troubleshooting

### Issue 1: Skill Not Found

**Problem:** `/jira-daily-report` command is not recognized

**Solutions:**
- Verify the file is at the correct location:
  - Global: `~/.claude/skills/jira-daily-report/SKILL.md`
  - Project: `.claude/skills/jira-daily-report/SKILL.md`
- Restart your editor/CLI
- Check the file has YAML frontmatter:
  ```markdown
  ---
  name: jira-daily-report
  description: ...
  ---
  ```

### Issue 2: Jira API Authentication Failed

**Problem:** "Unauthorized" or "403 Forbidden" error

**Solutions:**
1. Verify your Jira credentials are correct:
   ```bash
   curl -u $JIRA_USER:$JIRA_API_TOKEN \
        https://$JIRA_DOMAIN/rest/api/3/myself
   ```

2. Ensure environment variables are set:
   ```bash
   echo $JIRA_API_TOKEN
   echo $JIRA_USER
   ```

3. Check your Jira API token is valid:
   - Go to https://id.atlassian.com/manage/api-tokens
   - Verify your token hasn't expired
   - Create a new one if needed

4. Update credentials:
   ```bash
   export JIRA_API_TOKEN="new_token"
   export JIRA_USER="your_email@company.com"
   ```

### Issue 3: No Tasks Found

**Problem:** Skill runs but returns "No tasks found"

**Solutions:**
1. Verify the Jira link is correct:
   ```bash
   # Should point to your board or project
   https://your-company.atlassian.net/jira/board-key
   ```

2. Check the date range:
   ```
   /jira-daily-report https://your-company.atlassian.net/jira/board-key 2026-07-01 2026-07-15
   ```

3. Verify your user has access to the Jira board

4. Check your Jira JQL query permissions:
   ```bash
   curl -u $JIRA_USER:$JIRA_API_TOKEN \
        "https://$JIRA_DOMAIN/rest/api/3/search?jql=assignee%3DcurrentUser()"
   ```

### Issue 4: Permission Denied in Claude Code

**Problem:** "Permission denied" when trying to access `.claude/skills/`

**Solution:**
```bash
# Ensure proper permissions
chmod -R 755 ~/.claude/skills/
chmod -R 755 .claude/skills/
```

### Issue 5: Skill Works in Web but Not in Claude Code

**Problem:** Skill installed but not showing in Claude Code

**Solutions:**
1. Ensure you used the correct YAML frontmatter format (not markdown metadata)
2. Verify the file path:
   ```bash
   cat ~/.claude/skills/jira-daily-report/SKILL.md | head -10
   # Should show the YAML frontmatter starting with ---
   ```
3. Restart your editor completely
4. Try project-specific installation if global doesn't work

---

## Advanced Configuration

### Using with Jira Filters

To use your saved Jira filters:
```
/jira-daily-report https://your-company.atlassian.net/issues/?jql=filter=12345 2026-07-10 2026-07-15
```

### Customizing the Report Format

Edit the skill's `SKILL.md` file to modify:
- Report template sections
- Task filtering criteria
- Output formatting

---

## Support & Updates

For issues, questions, or updates:
- Check the main [README.md](../../README.md)
- Review the [SKILL.md](./SKILLs/jira-daily-report/SKILL.md) file for detailed execution guidelines
- Consult the [SKILLs README](./SKILLs/README.md) for usage examples

---

**Last Updated:** 2026-07-15
**Version:** 1.0
**Status:** ✅ Ready for Installation
