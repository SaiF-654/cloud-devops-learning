Real-Time Log Analysis Using sed in Linux
🧠 Objective:
To develop practical skills in using the sed command for text processing and automation, with a focus on real-world tasks faced by Cloud Administrators—such as editing config files, filtering logs, and updating scripts efficiently.



🏭 Industry Scenario:
You are working as a Junior DevOps Engineer at a cloud-based SaaS company. The production server logs need to be monitored daily to identify:
Error patterns
User login statistics
Request performance issues


Your job is to use Linux text processing tools (awk, sed, cut and grep) to extract insights from the logs and automate parts of the analysis.

✅ Prerequisites:
Running EC2 instance (Ubuntu)
Create IAM user
Give EC2 full permissions 
Access EC2 via IAM use



🔹 What is sed?
sed is a powerful stream editor used to perform basic text transformations on an input stream (a file or input from a pipeline). It is non-interactive, and is especially useful in scripting and automation.
It is used for finding and replacing, deleting, inserting, or editing lines in text files or streams


🔹 Basic Syntax

sed [options] 'command' filename



📁 Dummy Files
1. users.txt

john:x:1001:1001:John Doe:/home/john:/bin/bash
jane:x:1002:1002:Jane Smith:/home/jane:/bin/bash
Admin:x:0:0:Admin:/root:/bin/bash
john:x:1001:1001:John Doe:/home/john:/bin/bash
jane:x:1002:1002:Jane Smith:/home/jane:/bin/bash
Admin:x:0:0:Admin:/root:/bin/bash



2. webservers.txt

apache
nginx
docker
lighttpd
Nginx
apache


3. nginx.conf

server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://192.168.1.10:3000;
    }
}


4. access.log

192.168.0.1 - - [26/May/2025:10:15:42 +0000] "GET /index.html HTTP/1.1" 200
192.168.0.1 - - [26/May/2025:10:15:43 +0000] "GET /notfound HTTP/1.1" 404
192.168.0.1 - - [26/May/2025:10:15:44 +0000] "POST /login HTTP/1.1" 500


5. deploy.sh

#!/bin/bash
ENV=dev
PORT=3000
echo "Deploying application in $ENV environment on port $PORT"


6. security_rules.tf

resource "aws_security_group_rule" "ssh" {
  type        = "ingress"
  from_port   = 22
  to_port     = 22
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]
}


7. .env
DB_HOST=localhost
DB_USER=admin
DB_PASS=supersecret





8. os.txt

Linux is powerful.
Linux is open-source.
I prefer Linux over Windows.


9. logs.txt

INFO: Backup started.
ERROR: Database connection failed.
INFO: Retry connection.
ERROR: Timeout occurred.


10. start.sh

#!/bin/bash
echo "Starting the service..."


11. config.txt

environment=dev
region=us-west
path=/home/dev/us-west/app
backup=dev_backup_us-west.tar.gz

12. app.log
user=admin
password=MySecret123
status=active

user=test
password=test123
status=inactive


🧩 Part 1: Basics of sed

✅ 1. Print File Contents

sed '' users.txt
This just prints the file without modification (like cat).

✅ 2. Print Specific Line(s)
sed -n '3p' users.txt
🔹 Print only line 3.

sed -n '3,6p' users.txt
🔹 Print line 3 to 6.

✅ 3. Delete Line(s)

sed '3d' users.txt
🔹 Delete line 3.

sed '3,6d' users.txt
🔹 Delete lines 3 to 6.

✅ 4. Substitute (Replace Text)

sed 's/Admin/User/' users.txt
🔹 Replace first occurrence of “old” with “new” in each line.

sed 's/Admin/User/g' users.txt
🔹 Replace all occurrences.

🧩 Part 2: Intermediate sed Usage

✅ 5. In-place Editing (-i)

sed -i 's/apache/nginx/g' webservers.txt
🔹 Replace apache with nginx directly in the file.

✅ 6. Add Line Before or After Match

sed '/nginx/i BEFORE LINE' webservers.txt
🔹 Insert BEFORE LINE before any line matching nginx.

sed '/nginx/a AFTER LINE' webservers.txt
🔹 Append AFTER LINE after the matched line.

✅ 7. Replace Only on Specific Line(s)

sed '3s/docker/container/' webservers.txt
🔹 Only replace on line 3.

✅ 8. Use Regex Patterns

sed -n '/^error.*/p' logs.txt

🔹 Print lines starting with "error".

🧩 Part 3: Advanced sed Features

✅ 9. Multiple Commands

sed -e 's/dev/prod/g' -e 's/us-west/us-east/g' config.txt
🔹 Run multiple replacements in a single pass.

✅ 10. Save Output to New File

sed 's/Linux/Ubuntu/' os.txt > new_os.txt
🔹 Save transformed output to another file.

✅ 11. Use with Pipes

cat access.log | sed -n '/404/p'
🔹 Filter only 404 errors from logs.

🔐 Real-Time Use Cases for Cloud Admins

📌 1. Replace IP Address in Config File (e.g., nginx.conf)

sed -i 's/192.168.1.10/10.0.0.5/g' nginx.conf
✅ Update internal IPs when deploying in a different subnet.

📌 2. Change Port Numbers in Configurations

sed -i 's/80/8080/g' nginx.conf
✅ Quickly switch HTTP port for internal staging setup.

📌 3. Extract and Save EC2 Instance Logs with Errors

cat /var/log/syslog | sed -n '/error/p' > error-logs.txt
✅ Collect only relevant lines from remote log file.

📌 4. Automate Security Group Rules Update

sed -i 's/22/2222/' security_rules.tf
✅ Change SSH port in Terraform scripts before apply.

📌 5. Clean Up Sensitive Info in Logs

sed -i 's/password=.*/password=*****/g' /var/log/app.log
✅ Sanitize logs before sharing.

📌 6. Modify Environment Variables in .env File

sed -i 's/DB_HOST=.*/DB_HOST=prod-db.aws.com/' .env
✅ Seamless switching between environments.

📌 7. Add Logging in Init Scripts

sed -i '/^#!/a echo "Init started at $(date)"' start.sh
✅ Append a logging line after the shebang.

Tasks for your Practice
✅ 1. Change environment from dev to prod:
sed -i 's/ENV=dev/ENV=prod/' deploy.sh


✅ 2. Change port from 3000 to 8080:
sed -i 's/PORT=3000/PORT=8080/' deploy.sh


✅ 3. Insert a log line after the shebang:
sed -i '/^#!/a echo "=== Deployment Started at \$(date) ==="' deploy.sh


✅ 4. Append a new line at the end:
sed -i -e '$a echo "=== Deployment Complete ==="' deploy.sh


✅ 5. Comment out the echo line:
sed -i 's/^echo/#&/' deploy.sh
This adds # in front of lines starting with echo.


