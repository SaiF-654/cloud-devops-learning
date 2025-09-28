Backup and Restore Operations using Linux Archiving Commands (With Real-Time Output)

🎯 Objective
To simulate real-world backup and restoration using Linux archiving and compression tools like gzip, bzip2, zip, and tar.

🏢 Industry Scenario
You are a Junior DevOps Engineer at a SaaS firm. Your team needs you to archive logs and configs daily and restore them for debugging or audits.

📘 Assignment Tasks with Real-Time Output

Step 1: Create the Directory Structure
mkdir -p ~/backup-assignment/{app-logs,configs,docs,restored,extracted-raw,extracted-gz,extracted-bz2}

✅ Step 2: Create Dummy Files
# Log files
echo "ERROR: Disk space low" > ~/backup-assignment/app-logs/log1.txt
echo "INFO: Backup completed successfully" > ~/backup-assignment/app-logs/log2.txt


# Config files
echo "APP_PORT=8080" > ~/backup-assignment/configs/app.conf
echo "ENV=production" > ~/backup-assignment/configs/env.conf
# Docs
echo "This is the README file for backup instructions." > ~/backup-assignment/docs/readme.txt


✅ Verify Structure
tree ~/backup-assignment

💻 Expected Output:
backup-assignment
├── app-logs
│   ├── log1.txt
│   └── log2.txt
├── configs
│   ├── app.conf
│   └── env.conf
├── docs
│   └── readme.txt
├── restored
├── extracted-raw
├── extracted-gz
└── extracted-bz2

🔹 Task 1: Create and Extract tar Archives
✅ Create tar archive

tar -cvf ~/backup-assignment/raw-backup.tar ~/backup-assignment/app-logs ~/backup-assignment/configs ~/backup-assignment/docs

💻 Output

home/student/backup-assignment/app-logs/
home/student/backup-assignment/app-logs/log1.txt
home/student/backup-assignment/app-logs/log2.txt
home/student/backup-assignment/configs/
home/student/backup-assignment/configs/app.conf
home/student/backup-assignment/configs/env.conf
home/student/backup-assignment/docs/
home/student/backup-assignment/docs/readme.txt

✅ View contents

tar -tvf ~/backup-assignment/raw-backup.tar

💻 Output

drwxr-xr-x student/student     0 2025-05-11 11:00 backup-assignment/app-logs/
-rw-r--r-- student/student    27 2025-05-11 11:00 backup-assignment/app-logs/log1.txt
-rw-r--r-- student/student    30 2025-05-11 11:00 backup-assignment/app-logs/log2.txt
drwxr-xr-x student/student     0 2025-05-11 11:00 backup-assignment/configs/
-rw-r--r-- student/student    15 2025-05-11 11:00 backup-assignment/configs/app.conf
-rw-r--r-- student/student    24 2025-05-11 11:00 backup-assignment/configs/env.conf
drwxr-xr-x student/student     0 2025-05-11 11:00 backup-assignment/docs/
-rw-r--r-- student/student    31 2025-05-11 11:00 backup-assignment/docs/readme.txt

✅ Extract tar

tar -xvf ~/backup-assignment/raw-backup.tar -C ~/backup-assignment/extracted-raw


🔹 Task 2: Compressed tar.gz and tar.bz2 Archives
✅ Create tar.gz

tar -czvf ~/backup-assignment/compressed-backup.tar.gz ~/backup-assignment/app-logs ~/backup-assignment/configs ~/backup-assignment/docs

💻 Output

home/student/backup-assignment/app-logs/
home/student/backup-assignment/app-logs/log1.txt
home/student/backup-assignment/app-logs/log2.txt
home/student/backup-assignment/configs/
home/student/backup-assignment/configs/app.conf
home/student/backup-assignment/configs/env.conf
home/student/backup-assignment/docs/
home/student/backup-assignment/docs/readme.txt

✅ Extract tar.gz

tar -xzvf ~/backup-assignment/compressed-backup.tar.gz -C ~/backup-assignment/extracted-gz


✅ Create tar.bz2

tar -cjvf ~/backup-assignment/compressed-backup.tar.bz2 ~/backup-assignment/app-logs ~/backup-assignment/configs

💻 Output

home/student/backup-assignment/app-logs/
home/student/backup-assignment/app-logs/log1.txt
home/student/backup-assignment/app-logs/log2.txt
home/student/backup-assignment/configs/
home/student/backup-assignment/configs/app.conf
home/student/backup-assignment/configs/env.conf

✅ Extract tar.bz2




========================================================

Summary / Conclusion
In this exercise, you learned to use key Linux commands for backup and restoration:
gzip & bzip2: For compressing individual files, with bzip2 offering better compression.


zip: Used to archive multiple files and directories while preserving structure.


tar: Essential for archiving directories and compressing with options like tar.gz and tar.bz2.


We simulated real-world backup tasks, including compressing, archiving, and restoring logs and configurations. These tools are crucial for DevOps to efficiently manage and recover critical files in production environments.



