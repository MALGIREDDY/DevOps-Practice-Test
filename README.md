<h1 style="background-color:#222; color:white; padding:15px; border-radius:10px; text-align:center;">
 Automated Backup Script — DevOps Bash Scripting Project
</h1>

This project is part of a **DevOps Practice Test**, where the goal is to automate the process of taking file backups using **Bash scripting**.  
It demonstrates core DevOps skills such as automation, configuration management, Git usage, and working with real-world directory structures.

---

<h2 style="background-color:#222; color:white; padding:8px; border-radius:6px;">
 Project Objective
</h2>

In real DevOps environments, engineers often need to back up important files, configurations, or logs regularly.  
Manual backups are inefficient and prone to human error.

**Purpose:** Develop an automated solution that:
- Takes backups of any user-specified folder  
- Reads backup settings dynamically from a configuration file  
- Skips unnecessary files and folders (like `.git`, `node_modules`, `.cache`)  
- Supports a **Dry Run** mode to preview actions  
- Logs all actions for traceability  
- Demonstrates proper DevOps workflow with Git and GitHub  

---

<h2 style="background-color:#222; color:white; padding:8px; border-radius:6px;">
📁 Repository Overview
</h2>

<pre>
DevOps-Practice-Test/
│
├── bash-scripting_test/
│   └── test-1/
│       ├── backup.sh          # Main automation script
│       ├── backup.config      # Configuration file for backup parameters
│       └── README.md          # Documentation for this project
│
├── screenshots/               # Output examples and visuals
└── backup.logs/               # Log files of backup activity
</pre>

---

<h2 style="background-color:#222; color:white; padding:8px; border-radius:6px;">
 Files Explanation
</h2>

**1. backup.sh**  
Main Bash automation script that performs backup operations.  
**Functions include:**
- Checking configuration file availability  
- Reading backup parameters dynamically  
- Creating compressed `.tar.gz` archives  
- Logging results in `backup.log`  
- Supporting `--dry-run` for simulation

**Key Bash Concepts Used:**
- Conditional statements (`if`, `else`)  
- Reading variables using `source`  
- Command-line arguments (`$1`, `$2`)  
- Logging and redirection (`>>`)  
- Timestamp generation using `date`  

---

**2. backup.config**  
Configuration file that defines dynamic parameters for the backup.

Example:
```bash
# Directory where backups will be saved
BACKUP_DESTINATION="/c/Users/Dell/Desktop/bash practice/backups"

# File or folder patterns to skip
EXCLUDE_PATTERNS=".git,node_modules,.cache"

# Log file location
LOG_FILE="backup.log"

👤 Author Details 

Name: MALGIREDDY SAIDEEP

Course: DevOps Practice Test

Instructor: FAVOUR LAWRENCE

GitHub Repo: https://github.com/MALGIREDDY/DevOps-Practice-Test

Date of Submission: November 2025
