# 🧠 Automated Backup Script — DevOps Bash Scripting Project

This project is part of a **DevOps Practice Test**, where the goal is to automate the process of taking file backups using **Bash scripting**.  
It demonstrates core DevOps skills such as automation, file handling, configuration management, Git usage, and working with real-world directory structures.

---

## 🎯 Project Objective

In a real DevOps environment, engineers often need to back up important files, configurations, or logs regularly.  
Manually doing this every time is inefficient and prone to errors.

**Purpose:** To develop an automated backup solution that:

- 📦 Takes backups of any folder provided by the user  
- ⚙️ Reads backup settings from a configuration file  
- 🚫 Skips unnecessary files and folders (like `.git`, `node_modules`, `.cache`)  
- 🧪 Supports a **Dry Run** mode to preview actions before real backup  
- 🪵 Logs all actions for traceability  
- 💡 Demonstrates proper DevOps workflow using Git and GitHub  

---

## 📁 Repository Overview

DevOps-Practice-Test/
│
├── bash-scripting_test/
│ └── test-1/
│ ├── backup.sh # Main automation script
│ ├── backup.config # Configuration file for backup parameters
│ └── README.md # Documentation for the project
│
├── README.md # Root-level detailed project explanation
└── ...

markdown
Copy code

---

## ⚙️ Files Explanation

### 1️⃣ **backup.sh**
The main Bash script that performs the backup operation.

It:
- Checks if the `backup.config` file exists  
- Reads configuration variables (destination, exclusions, etc.)  
- Creates compressed `.tar.gz` backups with timestamps  
- Logs backup results into `backup.log`  
- Supports `--dry-run` mode to preview actions  

**Key Bash concepts used:**
- Conditional statements (`if`, `else`)  
- Reading variables using `source`  
- Command-line arguments (`$1`, `$2`)  
- Logging and redirection  
- String manipulation and timestamp generation using `date`  

---

### 2️⃣ **backup.config**
This configuration file makes the script **dynamic**, so users don’t need to modify the script itself.

**Example:**
```bash
# Directory where backups will be saved
BACKUP_DESTINATION="/c/Users/Dell/Desktop/bash practice/backups"

# File or folder patterns to skip during backup
EXCLUDE_PATTERNS=".git,node_modules,.cache"

# Log file location
LOG_FILE="backup.log"
🚀 How to Run the Project
1️⃣ Open Git Bash and go to your project directory:
bash
Copy code
cd "/c/Users/Dell/Desktop/bash practice/DevOps-Practice-Test/bash-scripting_test/test-1"
2️⃣ Give execute permissions to the script:
bash
Copy code
chmod +x backup.sh
3️⃣ Run in Dry Run Mode (to test without actual backup):
bash
Copy code
./backup.sh --dry-run /path/to/source/folder
Example Output:

bash
Copy code
[INFO] Dry run mode enabled
[INFO] Would backup folder: /home/user/documents
[INFO] Would save backup to: /c/Users/Dell/Desktop/bash practice/backups
[INFO] Would skip patterns: .git,node_modules,.cache
4️⃣ Run the Actual Backup:
bash
Copy code
./backup.sh /path/to/source/folder
Example Output:

bash
Copy code
[INFO] Starting backup process...
[INFO] Backup created successfully: /c/Users/Dell/Desktop/bash practice/backups/documents_backup_2025-11-03_11-30-15.tar.gz
[INFO] Backup log updated in backup.log
📂 Output Example
After running the backup, your destination folder (/backups) will look like this:

lua
Copy code
backups/
├── documents_backup_2025-11-03_11-30-15.tar.gz
├── pictures_backup_2025-11-03_11-32-07.tar.gz
└── backup.log
🧾 Logging Example (backup.log)
csharp
Copy code
[2025-11-03 11:30:15] Backup started for /home/user/documents
[2025-11-03 11:30:17] Backup completed successfully -> documents_backup_2025-11-03_11-30-15.tar.gz
This helps track backup history and troubleshooting.

🧩 DevOps Concepts Learned
Concept	Description
Automation	Created an automatic backup process using Bash
Configuration Management	Used backup.config for dynamic behavior
Scripting Skills	Practiced conditionals, loops, variables, and arguments
Version Control (Git)	Cloned, committed, and pushed project to GitHub
Testing	Used --dry-run to verify results
Logging	Implemented logging for debugging and record-keeping

🪄 Real-World Use Cases
This type of automation can be used by:

DevOps Engineers to back up configuration files from servers

Developers to save project snapshots daily

System Administrators for automated periodic backups

Teams practicing GitOps or CI/CD scripting

🧰 Tools & Technologies Used
🐚 Bash Shell Scripting

🌐 Git & GitHub

💻 Linux Command-Line (Git Bash on Windows)

📦 Tar and Gzip utilities

⚙️ Configuration-based Automation

🖼️ Screenshots
1️⃣ Project Folder Structure
Shows all files including backup.sh, backup.config, and backups folder.


2️⃣ Script Execution (Terminal Output)
Displays terminal output when running the script successfully.


3️⃣ Backups Folder
Shows the generated .tar.gz backup files saved in the destination folder.


4️⃣ Backup Log File
Displays log entries confirming backup creation and verification.


5️⃣ Dry Run Example
Previews how the script behaves in --dry-run mode.


🧩 Step-by-Step Explanation of Each Section
1️⃣ Dry Run Mode
yaml
Copy code
[2025-11-04 12:10:51] INFO: Dry run mode enabled
[2025-11-04 12:10:51] INFO: Would backup folder: /c/Users/Dell/Desktop/test_backup/data
[2025-11-04 12:10:51] INFO: Would save backup to: /c/Users/Dell/Desktop/bash practice/backups
[2025-11-04 12:10:51] INFO: Would skip patterns: .git,node_modules,.cache
✅ Confirms configuration and paths before actual execution.

2️⃣ Backup Start
swift
Copy code
[2025-11-04 12:11:02] INFO: Starting backup of /c/Users/Dell/Desktop/test_backup/data
Marks the beginning of the real backup process.

3️⃣ Backup Archive Created
bash
Copy code
[2025-11-04 12:11:03] SUCCESS: Backup created: /c/Users/Dell/Desktop/bash practice/backups/backup-2025-11-04-1211.tar.gz
✅ A compressed .tar.gz archive was successfully generated.

4️⃣ Checksum Saved
bash
Copy code
[2025-11-04 12:11:04] INFO: Checksum saved: /c/Users/Dell/Desktop/bash practice/backups/backup-2025-11-04-1211.tar.gz.md5
Ensures file integrity using MD5 checksum verification.

5️⃣ Checksum Verification
yaml
Copy code
[2025-11-04 12:11:04] SUCCESS: Checksum verified successfully.
Confirms that backup is not corrupted.

6️⃣ Backup Rotation Policy
yaml
Copy code
[2025-11-04 12:11:04] INFO: Applying backup rotation policy...
[2025-11-04 12:11:05] INFO: No old backups to delete.
Applies retention logic to keep backups manageable.

7️⃣ Integrity Test
yaml
Copy code
[2025-11-04 12:11:05] INFO: Testing backup integrity...
[2025-11-04 12:11:05] SUCCESS: Backup verified and ready!
Ensures that the backup archive can be opened and read properly.

8️⃣ Final Status
swift
Copy code
[2025-11-04 12:11:05] SUCCESS: Backup completed successfully for /c/Users/Dell/Desktop/test_backup/data
✅ Backup process finished without errors — backup is complete, verified, and safe 🎉

🧩 Design Decisions
Used Bash scripting for portability and Linux compatibility

Chose .tar.gz for efficient compression

Implemented MD5 checksum for backup integrity

Used backup.config for flexibility

Added lock file (/tmp/backup.lock) to prevent duplicate runs

Timestamp-based naming for easy version tracking

⚠️ Known Limitations
Incremental backups not yet implemented (full backups only)

Email notifications simulated (logs only)

Designed for local backups (S3/FTP support not added yet)

Tested mainly in Git Bash / Linux environments

🧠 Summary (Quick Explanation)
“First, the script runs in dry run mode to show what will be backed up.
Then it creates a compressed .tar.gz backup file and generates an MD5 checksum to verify integrity.
The checksum validation confirms that the file is not corrupted.
Next, it applies a rotation policy to manage backups, tests archive integrity, and finally confirms successful completion.”

👤 Author Details
Name: MALGIREDDY SAIDEEP

Course: DevOps Practice Test

Instructor: (Add your instructor’s name if applicable)

GitHub Repo: https://github.com/MALGIREDDY/DevOps-Practice-Test

Date of Submission: November 2025