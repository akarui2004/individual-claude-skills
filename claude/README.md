# Claude Skills Installation

## Installation via Claude Web

### Step 1: Format the `SKILL.md` file
To ensure Claude successfully recognizes and activates your custom skill, the file must begin with a structured metadata header. Use the template below to format your file:
```markdown
## Metadata
name: Your Skill Name (Maximum 64 characters)
description: A brief description of what the skill does and when Claude should activate it (Maximum 200 characters).
dependencies: python>=3.8, pandas>=1.5.0 (Specify required libraries if the skill executes code; otherwise, omit this line)

## Overview
(Provide a detailed explanation of the skill, including step-by-step instructions and guidelines...)
```
### Step 2: Package Your Skill into a ZIP Archive
Claude.ai requires your skill files to be organized inside a folder before being compressed. Follow these steps to package it correctly:
1. Create a dedicated folder: Name this folder after your skill (e.g., your-skill-name).
2. Rename and move your file: Rename your custom skill file to exactly SKILL.md (all caps) and place it inside the folder you just created.
3. Compress to ZIP: Zip the entire folder to create a .zip file (e.g., your-skill-name.zip).

### Step 3: Upload to `claude.ai`
1. Go to Claude.ai and log into your account
2. Make sure code execution is turned on. Go to Settings > Capabilities and toggle on Code execution and file creation.
3. In the left sidebar menu, click on Customize and select the Skills tab.
4. Click the "+" button (or + Create skill) and select Upload a skill.
5. Upload your .zip file containing the formatted skill.
6. Toggle the switch to Enable the skill. Now, whenever you start a chat related to this task, Claude will automatically activate and run the skill!

-----------------------------------

## Installation via Claude Code (Especially for VSCode, and CLI)

### Step 1: Format the SKILL.md File with YAML Frontmatter
For Claude Code, you must declare the metadata block using YAML format at the very beginning of your file:
```markdown
---
name: your-skill-name
description: A detailed description of when Claude Code should automatically trigger this skill.
---
# Your detailed instructions and steps start here...
```

### Step 2: Place the File in Claude's System Directory
Simply move your `SKILL.md` file into the appropriate Claude configuration folder:

1. Global (Applies to all projects) - Save the file at: ~/.claude/skills/<your-skill-folder-name>/SKILL.md
2. Project-specific (Applies to the current project only) - Save the file at: .claude/skills/<your-skill-folder-name>/SKILL.md directly in the root directory of your project.

### Step 3: Launch and Run
Start a new Claude Code session by typing the claude command in your terminal. Claude will automatically load your new skill.

1. You can type `/your-skill-name` to manually force-trigger the skill.
2. Alternatively, Claude will automatically detect and run the skill based on the description you defined when you input a relevant prompt.