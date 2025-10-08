Real-Time Log Analysis Using grep in Linux
🧠 Objective:
Understand and apply the grep command to search for specific text patterns in system and application log files.
Learn to use grep with various options, including regular expressions, to filter logs efficiently.
Analyze real-time server logs to detect errors, security events, configuration issues, and recurring patterns.	
Perform log monitoring tasks relevant to cloud-based production environments.
Begin automating routine log analysis using command-line tools like grep, awk, sed and cut.


🏭 Industry Scenario:
You are a Junior DevOps Engineer at a cloud-based SaaS company managing multiple AWS EC2 instances. Your role involves monitoring production logs daily to detect system errors, failed login attempts, and misconfigurations.
To streamline this process, you use grep, along with tools like awk and sed, to:
Filter errors and warnings from logs
Audit security events (e.g., SSH access)
Validate configuration files
Automate log analysis tasks


This helps maintain system reliability and security in a fast-paced, cloud-native environment.

✅ Prerequisites:
Running EC2 instance (Ubuntu)
Create IAM user
Give EC2 full permissions 
Access EC2 via IAM use

📁 Dummy Files
📁 1. syslog.log

sudo tee /home/ubuntu/syslog.log > /dev/null <<EOF
May 29 10:32:16 ip-172-31-12-45 systemd[1]: Started Session 4 of user ubuntu.
May 29 10:33:18 ip-172-31-12-45 sshd[1234]: Failed password for invalid user root from 192.168.1.10 port 54822 ssh2
May 29 10:35:20 ip-172-31-12-45 sshd[1234]: Accepted password for ubuntu from 192.168.1.11 port 54823 ssh2
May 29 10:36:21 ip-172-31-12-45 nginx[4321]: error: failed to connect to upstream
May 29 10:37:22 ip-172-31-12-45 nginx[4321]: warning: connection timeout
May 29 10:38:23 ip-172-31-12-45 systemd[1]: Reached target Timers.
EOF


📁 2. auth.log
sudo tee /home/ubuntu/auth.log > /dev/null <<EOF
May 29 10:33:18 ip-172-31-12-45 sshd[1234]: Failed password for root from 10.0.0.5 port 22 ssh2
May 29 10:35:20 ip-172-31-12-45 sshd[1234]: Accepted password for ubuntu from 10.0.0.6 port 22 ssh2
May 29 10:36:21 ip-172-31-12-45 sshd[1234]: Failed password for invalid user admin from 10.0.0.7 port 22 ssh2
May 29 10:36:22 ip-172-31-12-45 sshd[1234]: Accepted publickey for ubuntu from 10.0.0.6 port 22 ssh2
EOF


📁 3. sshd_config
sudo tee /home/ubuntu/sshd_config > /dev/null <<EOF
Port 22
PermitRootLogin yes
PasswordAuthentication yes
ChallengeResponseAuthentication no
UsePAM yes
EOF


📁 4. security_groups.csv
sudo tee /home/ubuntu/security_groups.csv > /dev/null <<EOF
GroupName,Protocol,PortRange,CIDR
web-sg,tcp,80,0.0.0.0/0
web-sg,tcp,22,192.168.0.0/24
db-sg,tcp,3306,10.0.0.0/16
admin-sg,tcp,22,0.0.0.0/0
EOF




📌 Part 1: grep Command
✅ What is grep?
grep stands for Global Regular Expression Print. It is used to search for text patterns in files or outputs.
It is a powerful, efficient tool for real-time log analysis, system debugging, and data extraction in Linux environments.

🔰 Basic Syntax:

grep [options] pattern [file...]


🧪 Basic Examples:
🔹 Example 1: Find a word in a file
grep "error" /var/log/syslog
🧾 Output: Lines containing the word error.

🔹 Example 2: Case-insensitive search
grep -i "error" /var/log/syslog

🔹 Example 3: Display line numbers
grep -n "failed" /var/log/auth.log

🔹 Example 4: Search recursively in a directory
grep -r "PermitRootLogin" /etc/ssh/

⚙️ Intermediate Usage:
🔹 Example 5: Invert match (exclude pattern)
grep -v "127.0.0.1" /etc/hosts

🔹 Example 6: Show only matched part
grep -o "error.*" /var/log/syslog

🔹 Example 7: Use with regular expressions
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" /var/log/syslog
🔍 Finds IP addresses.
🚀 Advanced Usage:
🔹 Example 8: Use with ps to filter processes
ps aux | grep nginx

🔹 Example 9: Count occurrences
grep -c "sshd" /var/log/auth.log

🔹 Example 10: Highlight results
grep --color=auto "ssh" /var/log/auth.log


💼 Cloud Admin Use Cases for grep
🧰 Use Case 1: Monitor EC2 logs for success
grep "SUCCESS" /var/log/cloud-init.log

🧰 Use Case 2: Check user login attempts
grep "Accepted" /var/log/auth.log

🧰 Use Case 3: Filter security group rules (in exported CSVs or configs)
grep "0.0.0.0/0" security_groups.csv

🧰 Use Case 4: Scan configuration files for weak settings
grep -E "PermitRootLogin|PasswordAuthentication" /etc/ssh/sshd_config


