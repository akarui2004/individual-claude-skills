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

   **Linux/macOS:**
   ```bash
   export JIRA_API_TOKEN="your_jira_api_token"
   export JIRA_USER="your_email@company.com"
   export JIRA_DOMAIN="your-company.atlassian.net"
   ```

   **Windows (PowerShell):**
   ```powershell
   $env:JIRA_API_TOKEN="your_jira_api_token"
   $env:JIRA_USER="your_email@company.com"
   $env:JIRA_DOMAIN="your-company.atlassian.net"
   ```

   **Windows (Command Prompt):**
   ```cmd
   set JIRA_API_TOKEN=your_jira_api_token
   set JIRA_USER=your_email@company.com
   set JIRA_DOMAIN=your-company.atlassian.net
   ```

### 3. **Jira CLI (Optional)**
   For enhanced functionality, install the Jira CLI:

   **macOS (Homebrew):**
   ```bash
   brew install jira-cli
   ```

   **Linux:**
   ```bash
   curl -L https://github.com/go-jira/jira/releases/download/v1.0.27/jira-linux-amd64 -o /usr/local/bin/jira
   chmod +x /usr/local/bin/jira
   ```

   **Windows (Chocolatey):**
   ```powershell
   choco install jira-cli
   ```

   **Windows (Manual Download):**
   1. Download from https://github.com/go-jira/jira/releases (jira-windows-amd64.exe)
   2. Add the executable to your PATH or use the full path when running

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

**Linux/macOS:**
1. **Create the skill directory:**
   ```bash
   mkdir -p ~/.claude/skills/jira-daily-report
   ```

2. **Copy the SKILL.md file:**
   ```bash
   cp /path/to/MyAISkills/claude/SKILLs/jira-daily-report/SKILL.md \
      ~/.claude/skills/jira-daily-report/SKILL.md
   ```

**Windows (PowerShell):**
1. **Create the skill directory:**
   ```powershell
   New-Item -ItemType Directory -Path "$env:APPDATA\.claude\skills\jira-daily-report" -Force
   ```

2. **Copy the SKILL.md file:**
   ```powershell
   Copy-Item -Path "C:\path\to\MyAISkills\claude\SKILLs\jira-daily-report\SKILL.md" `
             -Destination "$env:APPDATA\.claude\skills\jira-daily-report\SKILL.md"
   ```

**Windows (Command Prompt):**
1. **Create the skill directory:**
   ```cmd
   mkdir "%APPDATA%\.claude\skills\jira-daily-report"
   ```

2. **Copy the SKILL.md file:**
   ```cmd
   copy "C:\path\to\MyAISkills\claude\SKILLs\jira-daily-report\SKILL.md" "%APPDATA%\.claude\skills\jira-daily-report\SKILL.md"
   ```

3. **Verify the file exists:**

   **Linux/macOS:**
   ```bash
   ls -la ~/.claude/skills/jira-daily-report/
   ```

   **Windows (PowerShell):**
   ```powershell
   Get-ChildItem "$env:APPDATA\.claude\skills\jira-daily-report"
   ```

   **Windows (Command Prompt):**
   ```cmd
   dir "%APPDATA%\.claude\skills\jira-daily-report"
   ```

4. **Restart Claude Code** (VSCode, CLI, or other):
   - Close and reopen your editor
   - The skill should now be available

### Option B: Project-Specific Installation

Install the skill for a single project only:

**Linux/macOS:**
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

**Windows (PowerShell):**
1. **Create the skill directory in your project:**
   ```powershell
   New-Item -ItemType Directory -Path ".claude\skills\jira-daily-report" -Force
   ```

2. **Copy the SKILL.md file:**
   ```powershell
   Copy-Item -Path "C:\path\to\MyAISkills\claude\SKILLs\jira-daily-report\SKILL.md" `
             -Destination ".claude\skills\jira-daily-report\SKILL.md"
   ```

3. **Verify the file exists:**
   ```powershell
   Get-ChildItem ".claude\skills\jira-daily-report"
   ```

**Windows (Command Prompt):**
1. **Create the skill directory in your project:**
   ```cmd
   mkdir ".claude\skills\jira-daily-report"
   ```

2. **Copy the SKILL.md file:**
   ```cmd
   copy "C:\path\to\MyAISkills\claude\SKILLs\jira-daily-report\SKILL.md" ".claude\skills\jira-daily-report\SKILL.md"
   ```

3. **Verify the file exists:**
   ```cmd
   dir ".claude\skills\jira-daily-report"
   ```

4. **Restart Claude Code** and open this project
   - The skill will now be available within this project only

### Step 3: Configure Jira Credentials (Claude Code)

For Claude Code to access your Jira instance, set up credentials:

#### Option 1: Use Environment Variables

**Linux/macOS (Bash):**
```bash
export JIRA_API_TOKEN="your_api_token"
export JIRA_USER="your_email@company.com"
```

**Windows (PowerShell):**
```powershell
$env:JIRA_API_TOKEN="your_api_token"
$env:JIRA_USER="your_email@company.com"
```

**Windows (Command Prompt):**
```cmd
set JIRA_API_TOKEN=your_api_token
set JIRA_USER=your_email@company.com
```

#### Option 2: Use Jira CLI Configuration
```bash
# Configure the Jira CLI
jira configure -H https://your-company.atlassian.net -u your_email@company.com -p your_api_token
```

#### Option 3: Create a `.env` File (Project-Specific)

**Linux/macOS:**
```bash
# In your project root
echo "JIRA_API_TOKEN=your_api_token" > .env
echo "JIRA_USER=your_email@company.com" >> .env
echo "JIRA_DOMAIN=your-company.atlassian.net" >> .env
```

**Windows (PowerShell):**
```powershell
# In your project root
@"
JIRA_API_TOKEN=your_api_token
JIRA_USER=your_email@company.com
JIRA_DOMAIN=your-company.atlassian.net
"@ | Out-File -FilePath ".env" -Encoding UTF8
```

**Windows (Command Prompt):**
```cmd
# In your project root
(
  echo JIRA_API_TOKEN=your_api_token
  echo JIRA_USER=your_email@company.com
  echo JIRA_DOMAIN=your-company.atlassian.net
) > .env
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
  - **Linux/macOS Global:** `~/.claude/skills/jira-daily-report/SKILL.md`
  - **Windows Global:** `%APPDATA%\.claude\skills\jira-daily-report\SKILL.md`
  - **Project:** `.claude/skills/jira-daily-report/SKILL.md` (all platforms)
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

   **Linux/macOS:**
   ```bash
   curl -u $JIRA_USER:$JIRA_API_TOKEN \
        https://$JIRA_DOMAIN/rest/api/3/myself
   ```

   **Windows (PowerShell):**
   ```powershell
   curl.exe -u "$env:JIRA_USER:$env:JIRA_API_TOKEN" "https://$env:JIRA_DOMAIN/rest/api/3/myself"
   ```

2. Ensure environment variables are set:

   **Linux/macOS:**
   ```bash
   echo $JIRA_API_TOKEN
   echo $JIRA_USER
   ```

   **Windows (PowerShell):**
   ```powershell
   Write-Output $env:JIRA_API_TOKEN
   Write-Output $env:JIRA_USER
   ```

   **Windows (Command Prompt):**
   ```cmd
   echo %JIRA_API_TOKEN%
   echo %JIRA_USER%
   ```

3. Check your Jira API token is valid:
   - Go to https://id.atlassian.com/manage/api-tokens
   - Verify your token hasn't expired
   - Create a new one if needed

4. Update credentials:

   **Linux/macOS:**
   ```bash
   export JIRA_API_TOKEN="new_token"
   export JIRA_USER="your_email@company.com"
   ```

   **Windows (PowerShell):**
   ```powershell
   $env:JIRA_API_TOKEN="new_token"
   $env:JIRA_USER="your_email@company.com"
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

   **Linux/macOS:**
   ```bash
   curl -u $JIRA_USER:$JIRA_API_TOKEN \
        "https://$JIRA_DOMAIN/rest/api/3/search?jql=assignee%3DcurrentUser()"
   ```

   **Windows (PowerShell):**
   ```powershell
   curl.exe -u "$env:JIRA_USER:$env:JIRA_API_TOKEN" "https://$env:JIRA_DOMAIN/rest/api/3/search?jql=assignee%3DcurrentUser()"
   ```

### Issue 4: Permission Denied in Claude Code

**Problem:** "Permission denied" when trying to access `.claude/skills/`

**Solution (Linux/macOS):**
```bash
# Ensure proper permissions
chmod -R 755 ~/.claude/skills/
chmod -R 755 .claude/skills/
```

**Solution (Windows):**
Windows typically handles permissions differently. If you encounter permission issues:
1. Run Command Prompt or PowerShell as Administrator
2. Delete and recreate the `.claude/skills/` directory
3. Verify the file is not locked by another application

### Issue 5: Skill Works in Web but Not in Claude Code

**Problem:** Skill installed but not showing in Claude Code

**Solutions:**
1. Ensure you used the correct YAML frontmatter format (not markdown metadata)
2. Verify the file path:

   **Linux/macOS:**
   ```bash
   cat ~/.claude/skills/jira-daily-report/SKILL.md | head -10
   # Should show the YAML frontmatter starting with ---
   ```

   **Windows (PowerShell):**
   ```powershell
   Get-Content "$env:APPDATA\.claude\skills\jira-daily-report\SKILL.md" -Head 10
   # Should show the YAML frontmatter starting with ---
   ```

   **Windows (Command Prompt):**
   ```cmd
   type "%APPDATA%\.claude\skills\jira-daily-report\SKILL.md" | findstr /n ".*" | more +2
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
