Automated Backup Script — DevOps Bash Scripting Project

This project is part of a DevOps Practice Test, where the goal is to automate the process of taking file backups using Bash scripting.
It demonstrates core DevOps skills such as automation, file handling, configuration management, Git usage, and working with real-world directory structures.

Project Objective

In a real DevOps environment, engineers often need to back up important files, configurations, or logs regularly.
Manually doing this every time is inefficient and prone to errors.

Purpose: To develop an automated backup solution that:

Takes backups of any folder provided by the user

Reads backup settings from a configuration file

Skips unnecessary files and folders (like .git, node_modules, .cache)

Supports a Dry Run mode to preview actions before real backup

Logs all actions for traceability

Demonstrates proper DevOps workflow using Git and GitHub

Repository Overview
DevOps-Practice-Test/
│
├── bash-scripting_test/
│   └── test-1/
│       ├── backup.sh          # Main automation script
│       ├── backup.config      # Configuration file for backup parameters
│       └── README.md          # Documentation for the project
│
├── README.md                  # Root-level detailed project explanation
└── ...

Files Explanation
1. backup.sh

The main Bash script that performs the backup operation.

It:

Checks if the backup.config file exists

Reads configuration variables (destination, exclusions, etc.)

Creates compressed .tar.gz backups with timestamps

Logs backup results into backup.log

Supports --dry-run mode to preview actions

Key Bash concepts used:

Conditional statements (if, else)

Reading variables using source

Command-line arguments ($1, $2)

Logging and redirection

String manipulation and timestamp generation using date

2. backup.config

This configuration file makes the script dynamic, so users don’t need to modify the script itself.

Example:

# Directory where backups will be saved
BACKUP_DESTINATION="/c/Users/Dell/Desktop/bash practice/backups"

# File or folder patterns to skip during backup
EXCLUDE_PATTERNS=".git,node_modules,.cache"

# Log file location
LOG_FILE="backup.log"

How to Run the Project

Step 1: Open Git Bash and go to your project directory:

cd "/c/Users/Dell/Desktop/bash practice/DevOps-Practice-Test/bash-scripting_test/test-1"


Step 2: Give execute permissions to the script:

chmod +x backup.sh


Step 3: Run in Dry Run Mode (to test without actual backup):

./backup.sh --dry-run /path/to/source/folder


Example Output:

[INFO] Dry run mode enabled
[INFO] Would backup folder: /home/user/documents
[INFO] Would save backup to: /c/Users/Dell/Desktop/bash practice/backups
[INFO] Would skip patterns: .git,node_modules,.cache


Step 4: Run the Actual Backup:

./backup.sh /path/to/source/folder


Example Output:

[INFO] Starting backup process...
[INFO] Backup created successfully: /c/Users/Dell/Desktop/bash practice/backups/documents_backup_2025-11-03_11-30-15.tar.gz
[INFO] Backup log updated in backup.log

Output Example

After running the backup, your destination folder will look like this:

backups/
├── documents_backup_2025-11-03_11-30-15.tar.gz
├── pictures_backup_2025-11-03_11-32-07.tar.gz
└── backup.log

Logging Example (backup.log)
[2025-11-03 11:30:15] Backup started for /home/user/documents
[2025-11-03 11:30:17] Backup completed successfully -> documents_backup_2025-11-03_11-30-15.tar.gz


This helps track backup history and troubleshooting.

DevOps Concepts Learned
Concept	Description
Automation	Created an automatic backup process using Bash
Configuration Management	Used backup.config for dynamic behavior
Scripting Skills	Practiced conditionals, loops, variables, and arguments
Version Control (Git)	Cloned, committed, and pushed project to GitHub
Testing	Used --dry-run to verify results
Logging	Implemented logging for debugging and record-keeping
Real-World Use Cases

This type of automation can be used by:

DevOps Engineers to back up configuration files from servers

Developers to save project snapshots daily

System Administrators for automated periodic backups

Teams practicing GitOps or CI/CD scripting

Tools & Technologies Used

Bash Shell Scripting

Git & GitHub

Linux Command-Line (Git Bash on Windows)

Tar and Gzip utilities

Configuration-based Automation

Step-by-Step Explanation of Each Section
1. Dry Run Mode
[2025-11-04 12:10:51] INFO: Dry run mode enabled
[2025-11-04 12:10:51] INFO: Would backup folder: /c/Users/Dell/Desktop/test_backup/data
[2025-11-04 12:10:51] INFO: Would save backup to: /c/Users/Dell/Desktop/bash practice/backups
[2025-11-04 12:10:51] INFO: Would skip patterns: .git,node_modules,.cache


Confirms configuration and paths before actual execution.

2. Backup Start
[2025-11-04 12:11:02] INFO: Starting backup of /c/Users/Dell/Desktop/test_backup/data

3. Backup Archive Created
[2025-11-04 12:11:03] SUCCESS: Backup created: /c/Users/Dell/Desktop/bash practice/backups/backup-2025-11-04-1211.tar.gz

4. Checksum Saved
[2025-11-04 12:11:04] INFO: Checksum saved: /c/Users/Dell/Desktop/bash practice/backups/backup-2025-11-04-1211.tar.gz.md5

5. Checksum Verification
[2025-11-04 12:11:04] SUCCESS: Checksum verified successfully.

6. Backup Rotation Policy
[2025-11-04 12:11:04] INFO: Applying backup rotation policy...
[2025-11-04 12:11:05] INFO: No old backups to delete.

7. Integrity Test
[2025-11-04 12:11:05] INFO: Testing backup integrity...
[2025-11-04 12:11:05] SUCCESS: Backup verified and ready!

8. Final Status
[2025-11-04 12:11:05] SUCCESS: Backup completed successfully for /c/Users/Dell/Desktop/test_backup/data

Design Decisions

Used Bash scripting for portability and Linux compatibility

Chose .tar.gz for efficient compression

Implemented MD5 checksum for backup integrity

Used backup.config for flexibility

Added lock file (/tmp/backup.lock) to prevent duplicate runs

Timestamp-based naming for easy version tracking

Known Limitations

Incremental backups not yet implemented (full backups only)

Email notifications simulated (logs only)

Designed for local backups (S3/FTP support not added yet)

Tested mainly in Git Bash / Linux environments

Summary (Quick Explanation)

The script runs in Dry Run Mode first to show what will be backed up.

Then it creates a compressed .tar.gz backup file.

Generates an MD5 checksum to verify integrity.

Applies a rotation policy to manage old backups.

Tests archive integrity.

Finally confirms successful completion.

Author Details

Name: MALGIREDDY SAIDEEP

Course: DevOps Practice Test

Instructor: FAVOUR LAWRENCE

GitHub Repo: https://github.com/MALGIREDDY/DevOps-Practice-Test

Date of Submission: November 2025