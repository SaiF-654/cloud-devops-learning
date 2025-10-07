Linux File & Log Management in a Real-Time Production Environment
Learning Objectives:
By the end of this class, you will be able to:
Perform real-time file and directory management tasks on a Linux-based server.
Monitor and manage log files using standard Linux tools.
Simulate a production scenario with system-generated logs.
Apply troubleshooting using logs.
Real-Life Industry Scenario:
You are working as a Cloud Support Engineer at a SaaS company. Your responsibilities include managing user data stored in directories and troubleshooting application issues using Linux logs. Today, the DevOps team has reported performance issues, and the Support team is requesting data backup for a specific user.
✅ Prerequisites:
Running EC2 instance (Ubuntu)
Create IAM user
Give EC2 full permissions 
Access EC2 via IAM use

📂 PART 1: Practical File Management Hands-On
🏢 Real-Life Scenario:
You are managing client data directories on a Linux server. Each client has their own folder with data and reports. Your job is to:
Set up the structure
Control access with permissions
Archive reports for backup



✅ Step-by-Step Instructions with Real Output
🧱 Step 1: Create Client Directories

sudo mkdir -p /opt/clients/client_alpha/{data,reports}
sudo mkdir -p /opt/clients/client_beta/{data,reports}
sudo mkdir -p /opt/clients/client_gamma/{data,reports}

📥 Output:

(no output means success)

🔧 Step 2: Create User Groups

sudo groupadd client_alpha
sudo groupadd client_beta
sudo groupadd client_gamma

👥 Step 3: Set Ownership & Permissions

sudo chown -R root:client_alpha /opt/clients/client_alpha
sudo chmod -R 770 /opt/clients/client_alpha

sudo chown -R root:client_beta /opt/clients/client_beta
sudo chmod -R 770 /opt/clients/client_beta

sudo chown -R root:client_gamma /opt/clients/client_gamma
sudo chmod -R 770 /opt/clients/client_gamma

📁 Output (Check using ls -l):

ls -ld /opt/clients/client_alpha

drwxrwx--- 3 root client_alpha 4096 May 12 10:01 /opt/clients/client_alpha


📄 Step 4: Create Dummy Files in data/

echo "user_id,score" | sudo tee /opt/clients/client_alpha/data/data1.csv > /dev/null

echo "1,98" >> /opt/clients/client_alpha/data/data1.csv
✅ Fix: Use tee with sudo to append safely:
echo "1,98" | sudo tee -a /opt/clients/client_alpha/data/data1.csv > /dev/null

================================================
sudo touch /opt/clients/client_alpha/data/data2.csv
sudo touch /opt/clients/client_alpha/data/data3.csv

✅ Fix: Allow directory traversal (execute permission) on parent directories
Run the following commands to allow traversal by the ubuntu user:
sudo chmod +x /opt
sudo chmod +x /opt/clients
sudo chmod +x /opt/clients/client_alpha
+x on a directory means users can "cd" into it or access files inside.

📥 Output:

cat /opt/clients/client_alpha/data/data1.csv

user_id,score
1,98


📦 Step 5: Archive All reports/ Folders

sudo tar -czvf client_reports_backup.tar.gz -C /opt/clients client_alpha/reports client_beta/reports client_gamma/reports

📦 Output:

client_alpha/reports/
client_beta/reports/
client_gamma/reports/

📤 Step 6: Move and Set Permissions

sudo mv client_reports_backup.tar.gz /opt/backups/
sudo chmod 444 /opt/backups/client_reports_backup.tar.gz

✅ Final Check:

ls -l /opt/backups/client_reports_backup.tar.gz

-r--r--r-- 1 root root 10240 May 12 10:10 /opt/backups/client_reports_backup.tar.gz


📜 PART 2: Practical Logs Management Hands-On
🏢 Real-Life Scenario:
Your server is under SSH brute-force attacks. You need to extract all SSH login attempts and summarize the log activity for analysis.

logrotate is a tool in Linux that helps manage your log files so they don’t become too big and fill your disk.
What does it do?
It can:
Rotate the log (rename it, start a new one)
Compress old logs to save space
Delete very old logs
Run a command (like restarting a service) after rotating the logs

✅ Step-by-Step Instructions with Real Output
🧭 Step 1: Navigate to Log Directory

cd /var/log

🗂️ Step 2: View System Log (Ubuntu)

sudo tail -n 10 /var/log/syslog

📥 Output Example:

May 12 10:12:01 ubuntu CRON[2101]: (root) CMD (test -x /etc/init.d/anacron && /etc/init.d/anacron start)
May 12 10:12:01 ubuntu systemd[1]: Starting Clean php session files...

Creating Log Files 
📁 Create Working Directory

mkdir -p /opt/log_reports
cd /opt/log_reports


🧾 Create auth.log (dummy log with SSH entries)

nano auth.log (open auth.log file with nano editor)

Paste the following content:
May 25 10:00:01 server sshd[1234]: Accepted password for alice from 192.168.0.2 port 54321 ssh2
May 25 10:00:02 server sshd[1234]: pam_unix(sshd:session): session opened for user alice by (uid=0)
May 25 10:05:17 server sshd[1235]: Failed password for root from 192.168.0.3 port 54322 ssh2
May 25 10:07:45 server sshd[1236]: Accepted password for bob from 192.168.0.4 port 54323 ssh2
May 25 10:07:46 server sshd[1236]: pam_unix(sshd:session): session opened for user bob by (uid=0)
May 25 10:10:55 server sshd[1237]: Accepted password for charlie from 192.168.0.5 port 54324 ssh2
May 25 10:10:56 server sshd[1237]: pam_unix(sshd:session): session opened for user charlie by (uid=0)

Save and exit (CTRL+O, ENTER, CTRL+X).


🛡️ Step 3: Filter SSH Logs

grep "sshd" /var/log/auth.log > /opt/log_reports/ssh_access.log

📥 Output Example (inside file):

May 12 10:15:32 ubuntu sshd[2154]: Accepted password for testuser from 192.168.1.15 port 53782 ssh2
May 12 10:15:33 ubuntu sshd[2154]: pam_unix(sshd:session): session opened for user testuser by (uid=0)


📃 Step 4: Extract Timestamp and Username

awk '/sshd.*Accepted/ {print $1, $2, $3, $9}' /opt/log_reports/ssh_access.log > /opt/log_reports/summary.log

📥 Output (inside summary.log):

May 12 10:15:32 testuser


📦 Step 5: Archive Logs

tar -czvf /opt/log_reports/log_archive.tar.gz -C /opt/log_reports ssh_access.log summary.log

📥 Output:

ssh_access.log
summary.log


🔁 Step 6: Simulate Log Rotation
Create a logrotate config file
Create a file /etc/logrotate.d/ssh_access:

sudo nano /etc/logrotate.d/ssh_access

Paste these below lines into created file
/opt/log_reports/ssh_access.log {
    size 10k
    daily
    rotate 4
    compress
    missingok
    notifempty
}
This Means:
The log rotates when it reaches 10 KB.
Keep 4 backups and delete old ones
Compress old logs
Do nothing if log is missing or empty

Simulate logrotate:
sudo logrotate -f /etc/logrotate.d/ssh_access

This means:
sudo: Run as admin
logrotate: Use the logrotate tool
-f: Force it to run now
/etc/logrotate.d/ssh_access: Use the rules written in this file

Verify the rotation
Then check if the rotation happened:
ls -l /var/log/demo*




