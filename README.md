<p align="center">
  <img src="https://img.icons8.com/color/96/000000/console.png" />
  <img src="https://img.icons8.com/color/96/000000/processor.png" />
  <img src="https://img.icons8.com/color/96/000000/cloud-sync.png" />
</p
 HEAD
<h1 align="center">Automated Backup System</h1>
<p align="center">Linux • Bash • DevOps Automation</p>

.This project is part of a DevOps Practice Test, where the goal is to automate the process of taking file backups using Bash scripting.
It demonstrates core DevOps skills such as automation, file handling, configuration management, Git usage, and working with real-world directory structures.
73a0a64 (Updated screenshots and README formatting)

<p align="center">
  <img src="https://img.shields.io/badge/Bash_Scripting-1F1F1F?style=for-the-badge&logo=gnubash&logoColor=white"/>
  <img src="https://img.shields.io/badge/Linux_Environment-000000?style=for-the-badge&logo=linux&logoColor=white"/>
  <img src="https://img.shields.io/badge/Automation-5C4EE5?style=for-the-badge&logo=githubactions&logoColor=white"/>
  <img src="https://img.shields.io/badge/DevOps_Practices-0066CC?style=for-the-badge"/>
</p>

---

#  Overview

The **Automated Backup System** is a Bash-based DevOps script designed to automate directory backups using:

- Timestamped compressed archives  
- Configuration-based execution  
- MD5 checksum integrity verification  
- Exclusion rules for unnecessary directories  
- Dry-run simulation mode  
- Rotation policy for backup cleanup  
- Dedicated logging for traceability  

This project showcases real DevOps engineering capabilities: automation, observability, shell scripting, and system reliability.

---

#  Repository Structure
```
DevOps-Practice-Test/
│
├── bash-scripting_test/
│   └── test-1/
│       ├── backup.sh
│       ├── backup.config
│       └── README.md
│
├── backup.logs/
└── screenshots/
```


#  Features

###  Backup Engine
- Creates `.tar.gz` compressed archives  
- Auto timestamp naming  
- Error handling and logging  

###  Dry Run (Simulation Mode)
View the entire backup plan without creating files.

###  Exclusion Filtering
Skip large/unwanted directories:
- `.git`
- `node_modules`
- `.cache`

###  Integrity Validation
MD5 checksum ensures archive consistency.

###  Logging System
Tracks:
- Backup start/end time  
- Created archive path  
- Errors/warnings  

###  Backup Rotation Policy
Automatically removes older backups.

---

## Configuration (backup.config)

BACKUP_DESTINATION="/path/to/backups"
EXCLUDE_PATTERNS=".git,node_modules,.cache"
LOG_FILE="backup.log"

yaml
Copy code

---

##  Usage

### 1️⃣ Move to project directory
cd DevOps-Practice-Test/bash-scripting_test/test-1

shell
Copy code

### 2️⃣ Provide executable permission
chmod +x backup.sh

shell
Copy code

### 3️⃣ Run Dry Run (Recommended First)
./backup.sh --dry-run /path/to/source

shell
Copy code

### 4️⃣ Run Actual Backup
./backup.sh /path/to/source

yaml
Copy code

---

##  Architecture Flow

```
INPUT
  ↓
CONFIG LOADER
  ↓
EXCLUSION ENGINE
  ↓
ARCHIVE CREATION (.tar.gz)
  ↓
CHECKSUM GENERATION (MD5)
  ↓
INTEGRITY VALIDATION
  ↓
ROTATION POLICY
  ↓
LOGGING SYSTEM
```

---

##  Backup Output Example

```
backups/
├── data_backup_2025-11-03_11-30-15.tar.gz
├── project_backup_2025-11-03_11-45-21.tar.gz
└── backup.log
```

---

##  Log Sample

```
[2025-11-03 11:30:17] Backup completed → data_backup_2025-11-03_11-30-15.tar.gz
```


yaml
Copy code

---

##  Skills Demonstrated

### DevOps Engineering  
- Automation design  
- Observability & logging  
- Backup strategy  
- Configuration management  

### Bash Scripting  
- Argument parsing  
- Pattern filtering  
- Tar/gzip operations  
- MD5 checksum  
- Lock-file handling  

### Linux Operations  
- File system handling  
- Logging logic  
- Error management  

---

##  Tools & Technologies

<p align="left">
  <img src="https://img.shields.io/badge/Bash-1f1f1f?style=flat&logo=gnubash&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-000000?style=flat&logo=linux&logoColor=white" />
  <img src="https://img.shields.io/badge/Git-F2524D?style=flat&logo=git&logoColor=white" />
  <img src="https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white" />
</p>

---

##  Limitations
- Full backups only (incremental not implemented)  
- No cloud upload (S3/Azure/GCP not added)  
- No alerting system (Slack/Email not implemented)  

---

Backup Execution
The following screenshot shows the backup being executed successfully:

![Screenshot](screenshots/Screenshot%201.png.png)


 HEAD
##  Author
**Name:** MALGIREDDY SAIDEEP  
**Assessment:** DevOps Practical Test  
**Instructor:** FAVOUR LAWRENCE  
**Repo:** https://github.com/MALGIREDDY/DevOps-Practice-Test  
**Submitted:** November 2025  

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

Author Details.....

Name: MALGIREDDY SAIDEEP

Course: DevOps Practice Test

Instructor: FAVOUR LAWRENCE

GitHub Repo: https://github.com/MALGIREDDY/DevOps-Practice-Test

Date of Submission: November 2025
 73a0a64 (Updated screenshots and README formatting)
