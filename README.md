# 🧰 Automated Backup Script — DevOps Practice Test

This repository contains a **Bash Automation Project** designed to demonstrate DevOps fundamentals — automation, backup management, and configuration handling.  
It was created as part of a **DevOps Bash Scripting Practice Test**.

---

##  Project Overview

The **Automated Backup Script** simplifies creating backups of any directory using a configuration file.  
It supports dry-run mode, exclusion patterns, logging, and customizable backup paths — all configurable without modifying the script.

This script simulates a **real-world DevOps use case**: automating file system operations in Linux environments.

---

##  Project Structure

bash-scripting_test/
└── test-1/
├── backup.sh # Main automation script
├── backup.config # Configuration file for paths & exclusions
├── README.md # Project documentation

yaml
Copy code

---

## ⚙️ Configuration File — `backup.config`

The `backup.config` file defines parameters for the backup process.

Example:
```bash
# Destination folder for backups
BACKUP_DESTINATION="/c/Users/Dell/Desktop/bash practice/backups"

# Patterns to exclude
EXCLUDE_PATTERNS=".git,node_modules,.cache"

# Optional log file
LOG_FILE="backup.log"
 Script Usage
🔹 Normal Backup
bash
Copy code
./backup.sh /path/to/source/folder
This command backs up the given source folder based on the rules from backup.config.

🔹 Dry Run Mode
bash
Copy code
./backup.sh --dry-run /path/to/source/folder
This shows what would be backed up — without actually copying any files.

Sample Output:

bash
Copy code
[INFO] Dry run mode enabled
[INFO] Would backup folder: /home/user/documents
[INFO] Would save backup to: /c/Users/Dell/Desktop/bash practice/backups
[INFO] Would skip patterns: .git,node_modules,.cache
 Output Example
After running the script, your backup destination folder will contain:

Copy code
backups/
└── documents_backup_2025-11-03_11-15-23.tar.gz
 Learning Objectives
This project helped me practice:

Bash scripting fundamentals

File system navigation and automation

Using configuration files in scripts

Handling user arguments (--dry-run, etc.)

Logging and dynamic backup creation

Real DevOps workflow with Git and GitHub

 Author
Name: MALGIREDDY SAIDEEP
Platform: DevOps Practice Test (Instructor: [Insert Instructor Name])
GitHub Repository: https://github.com/MALGIREDDY/DevOps-Practice-Test


