#  Automated Backup Script — DevOps Bash Scripting Project

This project is part of a **DevOps Practice Test** where the goal is to **automate the process of taking file backups using Bash scripting**.  
It demonstrates core DevOps skills like automation, file handling, configuration management, Git usage, and working with real-world directory structures.

---

## Project Objective

In a real DevOps environment, engineers often need to back up important files, configurations, or logs regularly.  
Manually doing this every time is inefficient and prone to errors.  

Hence, the purpose of this project is to **develop an automated backup solution** that:
- Takes backups of any folder provided by the user  
- Reads backup settings from a configuration file  
- Skips unnecessary files and folders (like `.git`, `node_modules`, `.cache`)  
- Supports a “Dry Run” mode to preview actions before running the real backup  
- Logs all actions for traceability  
- Demonstrates proper DevOps workflow using Git and GitHub

---

##  Repository Overview

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

yaml
Copy code

---

## ⚙️ Files Explanation

### 1. `backup.sh`
This is the **main Bash script** that performs the backup operation.  
It:
- Checks if the `backup.config` file exists  
- Reads the configuration file to get destination and exclusion rules  
- Creates compressed (`.tar.gz`) backups with timestamps  
- Logs backup results into `backup.log`  
- Supports `--dry-run` mode to preview actions  

**Key Bash concepts used:**
- Conditional statements (`if`, `else`)
- Reading variables using `source`
- String manipulation
- Command-line arguments (`$1`, `$2`)
- Logging and redirection
- Timestamps using `date` command

---

### 2. `backup.config`
This configuration file makes the script dynamic — so the user doesn’t have to edit the script every time.  
It stores variables used by `backup.sh`.

Example:
```bash
# Directory where backups will be saved
BACKUP_DESTINATION="/c/Users/Dell/Desktop/bash practice/backups"

# File or folder patterns to skip during backup
EXCLUDE_PATTERNS=".git,node_modules,.cache"

# Log file location
LOG_FILE="backup.log"
How to Run the Project
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
 Output Example
After running the backup, your destination folder (/backups) will look like this:

lua
Copy code
backups/
├── documents_backup_2025-11-03_11-30-15.tar.gz
├── pictures_backup_2025-11-03_11-32-07.tar.gz
└── backup.log
The .tar.gz files are compressed archives of your source directories.

 Logging Example (backup.log)
csharp
Copy code
[2025-11-03 11:30:15] Backup started for /home/user/documents
[2025-11-03 11:30:17] Backup completed successfully -> documents_backup_2025-11-03_11-30-15.tar.gz
This helps track backup history and troubleshooting.

🧩 DevOps Concepts Learned
Concept	Description
Automation	Created an automatic backup process using Bash
Configuration Management	Used backup.config to control script behavior dynamically
Scripting Skills	Practiced conditionals, loops, variables, functions, and arguments in Bash
Version Control (Git)	Cloned, committed, and pushed project to GitHub
Testing	Used --dry-run to verify results before execution
Logging	Implemented logging mechanism for debugging and record-keeping

🪄 Real-World Use Case
This type of automation can be used by:

DevOps Engineers to back up configuration files from servers

Developers to save project snapshots daily

System administrators to automate periodic folder backups

Teams practicing GitOps or CI/CD scripting

 Tools & Technologies Used
Bash Shell Scripting

Git & GitHub

Linux Command-Line (Git Bash on Windows)

Tar and Gzip utilities

Configuration-based Automation


---

### 1️⃣ Project Folder Structure
Shows all files including `backup.sh`, `backup.config`, and the backups folder.

![Folder Structure](./screenshots/screenshot1_folder_structure.png)

---

### 2️⃣ Script Execution (Terminal Output)
Displays the terminal output when running the backup script successfully.

![Terminal Output](./screenshots/screenshot2_terminal_output.png)

---

### 3️⃣ Backups Folder
Shows the generated `.tar.gz` backup files saved in the destination folder.

![Backups Folder](./screenshots/screenshot3_backups_folder.png)

---

### 4️⃣ Backup Log File
Shows log entries confirming backup creation and verification.

![Backup Log File](./screenshots/screenshot4_log_file.png)

---

### 5️⃣ Dry Run Example (Optional)
Displays how the script previews actions in `--dry-run` mode before performing backups.

![Dry Run Output](./screenshots/screenshot5_dryrun_output.png)

---


Step-by-step Explanation of Each Section
🧾 1. Dry Run Mode
[2025-11-04 12:10:51] INFO: Dry run mode enabled
[2025-11-04 12:10:51] INFO: Would backup folder: /c/Users/Dell/Desktop/test_backup/data
[2025-11-04 12:10:51] INFO: Would save backup to: /c/Users/Dell/Desktop/bash practice/backups
[2025-11-04 12:10:51] INFO: Would skip patterns: .git,node_modules,.cache


🔹 Meaning:
This part shows that the script was first tested in “dry run” mode — meaning no real backup was created, but it displayed what would happen if the script runs for real.

🔹 It verified:

The source folder path ✅

The destination folder path ✅

Skip patterns like .git, node_modules, .cache ✅

✅ Purpose: To confirm everything is configured correctly before actual backup starts.

💾 2. Backup Start
[2025-11-04 12:11:02] INFO: Starting backup of /c/Users/Dell/Desktop/test_backup/data


🔹 Meaning: The actual backup process began for the folder /c/Users/Dell/Desktop/test_backup/data.

📦 3. Backup Archive Created
[2025-11-04 12:11:03] SUCCESS: Backup created: /c/Users/Dell/Desktop/bash practice/backups/backup-2025-11-04-1211.tar.gz


🔹 Meaning: The folder’s data was compressed successfully into a .tar.gz archive.
🗂️ File created:
backup-2025-11-04-1211.tar.gz in the backups/ folder.

🔐 4. Checksum Saved
[2025-11-04 12:11:04] INFO: Checksum saved: /c/Users/Dell/Desktop/bash practice/backups/backup-2025-11-04-1211.tar.gz.md5


🔹 Meaning:
The script generated an MD5 checksum file (digital signature) for the backup file — used to verify integrity (to ensure it wasn’t corrupted or changed later).

🗂️ File created:
backup-2025-11-04-1211.tar.gz.md5

✅ 5. Checksum Verification
[2025-11-04 12:11:04] SUCCESS: Checksum verified successfully.


🔹 Meaning:
The script compared the generated MD5 hash with the actual file and confirmed they match — the backup is valid and not corrupted.

🔄 6. Backup Rotation Policy
[2025-11-04 12:11:04] INFO: Applying backup rotation policy...
[2025-11-04 12:11:05] INFO: No old backups to delete.


🔹 Meaning:
This checks if too many backups exist (for example, older than 7 days or more than 5 files).
In your case, there were no old backups to delete, so it kept everything.

🧠 7. Integrity Test
[2025-11-04 12:11:05] INFO: Testing backup integrity...
[2025-11-04 12:11:05] SUCCESS: Backup verified and ready!


🔹 Meaning:
The script tested whether the .tar.gz file can be opened and read properly — confirming that the backup archive is not broken.

🟢 8. Final Status
[2025-11-04 12:11:05] SUCCESS: Backup completed successfully for /c/Users/Dell/Desktop/test_backup/data


## 🧩 Design Decisions

- Used **Bash scripting** for portability and native Linux compatibility.
- Chose **.tar.gz** format for fast compression and easy restoration.
- Used **MD5 checksum** to ensure integrity of backups.
- Separated configuration into `backup.config` to make the script reusable for different users.
- Implemented a **lock file** (`/tmp/backup.lock`) to prevent multiple script runs.
- Adopted a **timestamp-based naming scheme** for clear version tracking.


## ⚠️ Known Limitations

- Incremental backups are not yet implemented (full backup every time).
- Email notification is simulated (writes to a log instead of sending).
- Currently designed for local backups; remote (S3/FTP) not supported.
- Tested primarily in Git Bash / Linux environment.



🔹 Meaning:
All steps finished without errors — your backup is complete, verified, and safe 🎉

🧠 Summary for You to Say (Example for explanation to others)

“First, the script ran in dry run mode to show what will be backed up and skipped.
Then it started the actual backup, created a compressed .tar.gz file, and generated an MD5 checksum to verify file integrity.
The checksum was validated successfully, confirming the backup file wasn’t corrupted.
Next, the script checked for old backups based on the rotation policy, found none to delete, and tested the backup integrity.
Finally, it confirmed the backup completed successfully.”


 Author Details
Name: MALGIREDDY SAIDEEP

Course: DevOps Practice Test

Instructor: (Your instructor’s name if applicable)

GitHub Repo: https://github.com/MALGIREDDY/DevOps-Practice-Test

Date of Submission: November 2025