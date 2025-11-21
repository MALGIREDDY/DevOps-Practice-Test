# Bash Scripting Project: Automated Backup System
---

## A. Project Overview

### 1. What does your script do?
This script automatically creates backups of any folder specified by the user.  
It compresses the folder into a `.tar.gz` archive, stores it in a backup directory, and logs all actions.  
It also generates an MD5 checksum to ensure that the backup file is not corrupted.

### 2. Why is it useful?
Manual backups can be time-consuming and error-prone.  
This automated tool ensures backups are:

- Reliable  
- Repeatable  
- Consistent  
- Verifiable  

This is important for system administrators, DevOps engineers, and anyone managing important files.

---

## B. How to Use It

### 1. Installation Steps
1. Download or clone the repository.  
2. Navigate to the project folder.  
3. Make the backup script executable:
```
chmod +x backup.sh
```
4. Configure your backup settings inside `backup.config`.

### 2. Basic Usage Examples

**Dry Run (recommended first):**
```
./backup.sh --dry-run /path/to/source
```

**Real Backup:**
```
./backup.sh /path/to/source
```

### 3. Command Options Explained
| Command     | Meaning                                         |
|-------------|--------------------------------------------------|
| `--dry-run` | Shows what will happen without creating a backup |
| No flags    | Creates the actual backup                       |

---

## Project Folder Structure

```
backup-system/
├── backup.sh
├── backup.config
├── README.md
└── screenshots/
    ├── screenshot1.png
```

---

## C. How It Works

### 1. Rotation Algorithm (Daily, Weekly, Monthly Retention)

To fully match the project requirements, the script must maintain three types of
retention policies:

- **7 Daily backups**
- **4 Weekly backups**
- **3 Monthly backups**

This ensures the system has recovery points across recent days, past weeks, and
past months.

#### How rotation works:

1. **Daily Retention (7 days)**
   - The script groups backups by date and keeps only the **newest backup from each of the last 7 days**.
   - Any additional backups created on the same day are deleted.

2. **Weekly Retention (4 weeks)**
   - From the last 4 weeks, the script keeps **one backup per week** (usually the most recent one).
   - Older weekly backups are removed.

3. **Monthly Retention (3 months)**
   - The script keeps **one backup from each of the last 3 months**.
   - Older monthly backups are deleted automatically.

#### Retention Settings (from backup.config)

```
DAILY_KEEP=7
WEEKLY_KEEP=4
MONTHLY_KEEP=3
```

#### Why this retention policy is needed?

This prevents the backup directory from growing endlessly while still keeping:

- Short-term backups (daily)
- Medium-term backups (weekly)
- Long-term backups (monthly)

This multi-level retention strategy matches real enterprise backup policies.

Steps:
1. Count existing backups.  
2. If the number exceeds the limit, delete the oldest backup.  

This ensures the backup folder does not grow too large.

### 2. Checksum Creation
Checksum is created to verify integrity:

```
md5sum backup.tar.gz > backup.tar.gz.md5
```

Verification:
```
md5sum -c backup.tar.gz.md5
```

### 3. Folder Structure for Backups
```
backups/
├── folder_backup_2025-11-03_11-30-15.tar.gz
├── folder_backup_2025-11-04_12-22-11.tar.gz
└── backup.log
```

---

## D. Design Decisions

### 1. Why this approach?
- Bash works on all Linux systems  
- Configuration file makes script flexible  
- tar + gzip = efficient and widely supported  
- Logging makes debugging easier  

### 2. Challenges faced
- Handling invalid paths  
- Deleting the correct backup during rotation  
- Ensuring checksum accuracy  
- Preventing script crashes  

### 3. Solutions applied
- Added input validation  
- Added rotation function  
- Added checksum verification  
- Added clear error messages  

---

## E. Testing

### How I tested the script

#### 1. Created a test folder:
```
mkdir test_backup
echo "File 1 content" > test_backup/file1.txt
echo "File 2 content" > test_backup/file2.txt
echo "Log file" > test_backup/logs.txt
```

#### 2. Tested Dry Run:
```
./backup.sh --dry-run test_backup
```

#### 3. Performed real backups:
```
./backup.sh test_backup
```

#### 4. Verified checksum:
Checked `.md5` file and validated the backup integrity.

#### 5. Tested rotation:
```
./backup.sh test_backup
sleep 2
./backup.sh test_backup
sleep 2
./backup.sh test_backup
```

#### 6. Error handling:
```
./backup.sh /invalid/folder
```

---

## Example Outputs

### Dry Run Output
```
[INFO] Dry run mode enabled
[INFO] Would backup folder: test_backup
[INFO] Would save archive to: backups/
[INFO] Would skip patterns: .git,node_modules,.cache
```

### Successful Backup Output
```
[2025-11-21 11:57:21] INFO: Starting backup of test_backup
[2025-11-21 11:57:21] SUCCESS: Backup created: backups/test_backup_2025-11-21-1157.tar.gz
[2025-11-21 11:57:22] INFO: Checksum saved
[2025-11-21 11:57:22] SUCCESS: Checksum verified successfully.
```

---

## F. Known Limitations

### What doesn't work yet
- Incremental backups  
- Cloud uploads (S3/Azure/GCP)  
- Email/Slack notifications  
- Restore command  
- Encryption  

### What could be improved
- Add incremental backups  
- Add restore functionality  
- Add cloud support  
- Add alerts/notifications  
- Improve log formatting  
- Add cron scheduling  

---

## G. Full Test Demonstrations

### 1. Creating a Backup
```
./backup.sh test_backup
```

### 2. Multiple Backups (Simulated Days)
```
./backup.sh test_backup
sleep 2
./backup.sh test_backup
sleep 2
./backup.sh test_backup
```

### 3. Automatic Rotation
```
[INFO] Applying backup rotation policy...
[INFO] Deleting oldest backup: test_backup_2025-11-21-1157.tar.gz
```

### 4. Restore Example (optional)
```
mkdir restore_output
tar -xzvf backups/test_backup_2025-11-21-1200.tar.gz -C restore_output/
```

### 5. Dry Run
```
./backup.sh --dry-run test_backup
```

### 6. Error Handling
```
ERROR: Source folder does not exist.
```

---

## Screenshot

### Backup Execution  
![Backup Execution](screenshots/screenshot1.png)

---
## I. Sample Log Output

Below is an example of the log entries generated during a full backup process.  
This shows the timestamp, status of each step, and confirms whether the backup succeeded.

```
[2025-11-21 11:57:21] INFO: Backup started for test_backup
[2025-11-21 11:57:21] INFO: Creating compressed archive...
[2025-11-21 11:57:21] SUCCESS: Backup archive created successfully
[2025-11-21 11:57:22] INFO: Generating checksum file
[2025-11-21 11:57:22] SUCCESS: Checksum saved
[2025-11-21 11:57:22] INFO: Verifying checksum integrity
[2025-11-21 11:57:22] SUCCESS: Checksum verified successfully
[2025-11-21 11:57:22] INFO: Applying rotation policy
[2025-11-21 11:57:22] INFO: No old backups to delete
[2025-11-21 11:57:23] SUCCESS: Backup completed successfully
```


## J. Final Tips and Learning Reflection
- I built and tested each feature step-by-step.  
- Using GitHub helped track my changes.  
- Error messages made debugging easier.  
- Functions improved readability.  
- Logging made the process transparent.  

I learned core DevOps concepts such as automation, configuration management, logging, scripting, and testing.

---

