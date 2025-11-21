# Bash Scripting Project: Automated Backup System
-----------------------------------------------

## A. Project Overview

### 1. What does your script do?
This script automatically creates backups of any folder that the user selects.  
It compresses the folder into a `.tar.gz` archive, stores it in a backup directory, and logs all actions.  
It also creates an MD5 checksum to verify that the backup file is not corrupted.

### 2. Why is it useful?
Manual backups take time and can lead to mistakes.  
Automating the process makes backups reliable, repeatable, and consistent.  
It also helps system administrators and DevOps engineers keep important data safe.

---

## B. How to Use It

### 1. Installation Steps
1. Download or clone the project repository.
2. Navigate to the project folder.
3. Make the script executable:
4. chmod +x backup.sh

4. Update the `backup.config` file with your destination folder and exclusion patterns.

---

### 2. Basic Usage Examples

### Dry run (no backup created)
```bash
./backup.sh --dry-run /path/to/source
```

### Real backup
```bash
./backup.sh /path/to/source
```


### 3. Command Options Explained

| Command     | Meaning                                          |
|-------------|--------------------------------------------------|
| `--dry-run` | Shows what will happen without creating a backup |
| No flags    | Creates the actual backup                        |

---
## Project Folder Structure
```
backup-system/
├── backup.sh
├── backup.config
├── README.md
└── screenshots/
    ├── screenshot1.png
    ├── screenshot2.png
```


## C. How It Works

### 1. Rotation Algorithm
The script keeps only a specific number of backups.  
When a new backup is created:
1. It counts all existing backups.  
2. If the number is greater than your retention limit, the oldest backup is deleted.  

This prevents the backup folder from becoming too large.

### 2. Checksum Creation

The script creates an MD5 checksum:


md5sum backup.tar.gz > backup.tar.gz.md5


Verification:


md5sum -c backup.tar.gz.md5


### 3. Folder Structure for Backups

```
backups/
├── folder_backup_2025-11-03_11-30-15.tar.gz
├── folder_backup_2025-11-04_12-22-11.tar.gz
└── backup.log
```


## D. Design Decisions

### 1. Why this approach?
- Bash works on all Linux systems  
- Configurable through `backup.config`  
- Tar & gzip create efficient compressed files  
- Logging helps in auditing and debugging  

### 2. Challenges faced
- Handling invalid paths  
- Ensuring rotation deletes the correct file  
- Verifying checksum accuracy  
- Avoiding script crashes due to incorrect inputs  

### 3. How challenges were solved
- Added folder validation  
- Added rotation function  
- Integrated checksum verification  
- Added clear error messages  

---

## E. Testing

### How did you test your script?
I tested the script using multiple real scenarios:

1. **Created a test folder with sample files**
```bash
mkdir test_backup
echo "File 1 content" > test_backup/file1.txt
echo "File 2 content" > test_backup/file2.txt
echo "Log file" > test_backup/logs.txt
```

2. **Tested Dry Run mode**
```bash
./backup.sh --dry-run test_backup
```

3. **Performed real backups**
```bash
./backup.sh test_backup
```

4. **Verified checksum and integrity**  
Checked the `.md5` file and ran extraction tests.


5. **Created multiple backups to test rotation**
```bash
./backup.sh test_backup
sleep 2
./backup.sh test_backup
sleep 2
./backup.sh test_backup
```

6. **Tested error handling**  
Attempted to back up a folder that does not exist:
```bash
./backup.sh /invalid/folder
```

### Example Outputs

**Dry run output**
```bash
[INFO] Dry run mode enabled
[INFO] Would backup folder: test_backup
[INFO] Would save archive to: backups/
[INFO] Would skip patterns: .git,node_modules,.cache
```

**Successful backup output**
```bash
[2025-11-21 11:57:21] INFO: Starting backup of test_backup
[2025-11-21 11:57:21] SUCCESS: Backup created: backups/test_backup_2025-11-21-1157.tar.gz
[2025-11-21 11:57:22] INFO: Checksum saved
[2025-11-21 11:57:22] SUCCESS: Checksum verified successfully.
```



## F. Known Limitations

### What doesn't work yet?
- Incremental backups (only full backups supported)
- Cloud uploads (S3, Azure, GCP not implemented)
- Email / Slack notifications not included
- No built-in restore command
- No encryption support

### What could be improved?
- Add incremental and differential backup support  
- Add restore-from-backup feature  
- Add cloud backup integration (S3, Azure Blob, GCP Storage)  
- Add notification alerts (email, Slack, Teams)  
- Improve logging system (JSON logs, log rotation)  
- Add automated scheduling using cron  


## G. Full Test Demonstrations (Required by Instructor)

### 1. Creating a Backup
```
./backup.sh test_backup
```

**Example Output**
```
[2025-11-21 11:57:21] INFO: Starting backup of test_backup
[2025-11-21 11:57:21] SUCCESS: Backup created: backups/test_backup_2025-11-21-1157.tar.gz
[2025-11-21 11:57:22] INFO: Checksum saved
[2025-11-21 11:57:22] SUCCESS: Checksum verified successfully.
```

---

### 2. Creating Multiple Backups (Simulated Over “Days”)
```
./backup.sh test_backup
sleep 2
./backup.sh test_backup
sleep 2
./backup.sh test_backup
```

**Example Output**
```
Created backups:
test_backup_2025-11-21-1157.tar.gz
test_backup_2025-11-21-1200.tar.gz
test_backup_2025-11-21-1202.tar.gz
```

---

### 3. Automatic Deletion of Old Backups (Rotation)
Assume retention limit = 3.

```
./backup.sh test_backup
```

**Output**
```
[INFO] Applying backup rotation policy...
[INFO] Deleting oldest backup: test_backup_2025-11-21-1157.tar.gz
```

---

### 4. Restoring from a Backup (Optional)
```
mkdir restore_output
tar -xzvf backups/test_backup_2025-11-21-1200.tar.gz -C restore_output/
```

**Restored Files**
```
file1.txt
file2.txt
logs.txt
```

---

### 5. Dry Run Mode
```
./backup.sh --dry-run test_backup
```

**Output**
```
[INFO] Dry run mode enabled
[INFO] Would backup folder: test_backup
[INFO] Would save archive to: backups/
[INFO] Would skip patterns: .git, node_modules, .cache
```

---

### 6. Error Handling Test
```
./backup.sh /invalid/folder
```

**Output**
```
ERROR: Source folder does not exist.
```
## Screenshots

### 1. Project Folder Screenshot
![Project Folder](screenshots/screenshot1.png)

### 2. Backup Execution (Optional but Recommended)
![Backup Execution](screenshots/screenshot2.png)

## G. How the Script Was Developed (Step-by-Step)

### 1. Starting Simple
The first version of the script only created a basic compressed backup:
```
tar -czf backup-test.tar.gz /path/to/folder
```
This helped ensure tar and gzip worked correctly.

### 2. Adding a Timestamp
To avoid overwriting backups, a timestamp was added:
```
TIMESTAMP=$(date +%Y-%m-%d-%H%M)
tar -czf backup-$TIMESTAMP.tar.gz /path/to/folder
```

### 3. Breaking Code into Functions
The script was then organized into functions for clarity:
```
create_backup() { ... }
verify_backup() { ... }
apply_rotation() { ... }
```

### 4. Adding Error Checking
Input validation was added:
```
if [ ! -d "$SOURCE_DIR" ]; then
    echo "Error: Directory does not exist"
    exit 1
fi
```

### 5. Adding Logging
A logging function was added:
```
log() {
    echo "[$(date "+%Y-%m-%d %H:%M:%S")] $1" >> backup.log
}
```

---
## H. Useful Commands Used in the Script
These are the key Linux commands used:

| Command      | Purpose |
|--------------|---------|
| `tar -czf`   | Create compressed archive |
| `tar -xzf`   | Extract backup |
| `md5sum`     | Create checksum |
| `md5sum -c`  | Verify checksum |
| `find`       | List and filter old backups |
| `sort`       | Sort backups by date |
| `wc -l`      | Count total backups |
| `date`       | Generate timestamps |
| `df -h`      | Check available disk space |

---
## I. Sample Log Output 
```
[2025-11-21 11:57:21] INFO: Backup started for test_backup
[2025-11-21 11:57:22] INFO: Backup file created successfully
[2025-11-21 11:57:22] INFO: Checksum saved
[2025-11-21 11:57:22] SUCCESS: Checksum verified successfully
[2025-11-21 11:57:22] INFO: Applying rotation policy
[2025-11-21 11:57:22] INFO: No old backups to delete
[2025-11-21 11:57:23] SUCCESS: Backup completed successfully
```

---
## J. Final Tips and Learning Reflection
- I tested each feature step-by-step instead of writing everything at once.  
- Using version control (GitHub) helped track changes and avoid mistakes.  
- Error messages made debugging easier and prevented crashes.  
- Breaking the script into functions improved organization and readability.  
- Logging made the backup process transparent and easy to review.  
- Overall, I learned core DevOps concepts: automation, logging, configuration, and Linux command usage.

