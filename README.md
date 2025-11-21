📦 Automated Backup System
A Bash-Scripting Based Backup Automation Project

This project was developed as part of the DevOps Practical Assessment.
It focuses on building a real-world backup automation utility using Bash — similar to tasks handled by DevOps and SRE engineers in production environments.

1. 🔍 Project Summary

Modern systems generate logs, configs, and data that need regular backups.
Manual backups cause errors and are not scalable.

This project implements an:

Automated Backup System with:

Dynamic configuration (via backup.config)

Compression of backup archives

Exclusion rules for unnecessary folders

Dry-run verification mode

Logging for auditing

Checksum validation

Backup retention

2. 🗂 Repository Structure
DevOps-Practice-Test/
│
├── bash-scripting_test/
│   └── test-1/
│       ├── backup.sh
│       ├── backup.config
│       └── README.md
│
├── screenshots/
└── backup.logs/

3. 🚀 Features Implemented
Backup Functionality

Backs up any directory provided as input

Creates compressed .tar.gz files

Generates MD5 checksums

Dry Run Mode (--dry-run)

Shows planned actions without performing backup

Helps prevent mistakes before actual runs

Exclusion Support

Skip unwanted directories like:

.git

node_modules

.cache

Logging

Every backup action is recorded in:

backup.log

Backup Rotation

Automatically removes older backups (based on policy).

4.  Configuration File (backup.config)

A simple configuration-driven design makes the script portable and reusable.

Example:

BACKUP_DESTINATION="/c/Users/Dell/Desktop/backups"
EXCLUDE_PATTERNS=".git,node_modules,.cache"
LOG_FILE="backup.log"

5. 🖥 How to Run
1. Navigate to project
cd "DevOps-Practice-Test/bash-scripting_test/test-1"

2. Give execution permissions
chmod +x backup.sh

3. Test in Dry Run Mode
./backup.sh --dry-run /path/to/folder

4. Run Actual Backup
./backup.sh /path/to/folder

6. 📁 Backup Output Example
backups/
├── documents_backup_2025-11-03_11-30-15.tar.gz
├── pictures_backup_2025-11-03_11-32-07.tar.gz
└── backup.log


Example Log Entry:

[2025-11-03 11:30:17] Backup completed -> documents_backup_2025-11-03_11-30-15.tar.gz

7. 🧠 Skills Demonstrated
Area	What I Implemented
Bash Automation	Full automated backup system
Linux Commands	tar, gzip, md5sum, directory checks
Config Management	Parameterization via backup.config
Logging	Detailed, timestamped logs
Testing	Dry-run mode
Git	Version control & GitHub repo setup
8. 📌 Design Decisions

Config-Driven → Script is reusable without modification

Checksum Validation → Ensures archive integrity

Rotation Policy → Prevents backup directory from growing indefinitely

Error Handling → Messages for missing folder, bad config, etc.

Lock File → Prevents multiple running instances

9. ⚠ Limitations

Only supports full backups, not incremental

No cloud storage backups yet (S3, GDrive, etc.)

Tested on Git Bash + Ubuntu; may vary slightly on other shells

10. 👨‍💻 Author

Name: MALGIREDDY SAIDEEP
Course: DevOps Practical Assessment
Instructor: FAVOUR LAWRENCE
GitHub: https://github.com/MALGIREDDY/DevOps-Practice-Test

Submission Date: November 2025



Premium Enterprise Documentation Style

Modern Developer Portfolio Style
