System Level Linux Commands in Real-World Scenario
🎯 Industry Scenario:
You are a Cloud Operations Engineer working in a company that hosts a web application on AWS using Ubuntu-based virtual machine (VM).
Objective:
Your task is to perform system diagnostics, monitor resources, manage packages, and control services on the server hosting the application

🛠️ Part 1: System Diagnostics and Monitoring
✅ Task 1.1: Print system information

uname -a
Expected Output:
Linux web-server01 5.15.0-105-generic #115-Ubuntu SMP x86_64 GNU/Linux

📌 This helps identify kernel version and architecture, useful when troubleshooting.

✅ Task 1.2: Display system’s hostname

hostname

Expected Output:

web-server01

📌 Useful for identifying the server in a cluster or inventory.

✅ Task 1.3: Check system uptime
uptime

Expected Output:

12:30:45 up 5 days,  4:17,  3 users,  load average: 0.25, 0.40, 0.36

📌 Important to check for unexpected reboots or downtime.

✅ Task 1.4: Check memory usage

free -h

Expected Output:

             total        used        free      shared  buff/cache   available
Mem:           3.8G        1.1G        500M        200M        2.2G        2.1G
Swap:            0B          0B          0B


✅ Task 1.5: Check disk space

df -h

Expected Output:

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        40G   15G   23G  40% /


📊 Part 2: Process and Resource Monitoring
✅ Task 2.1: Monitor processes (real-time)

top

📌 Interactive process viewer. Observe CPU and memory usage.

✅ Task 2.2: Use advanced monitoring (install htop)

sudo apt install htop
htop

📌 Better visual representation of processes. Sort by memory, CPU.

✅ Task 2.3: Find specific process (e.g., SSH)

ps aux | grep ssh

Expected Output:

root       1011  0.0  0.1  12964  5252 ?        Ss   10:00   0:00 /usr/sbin/sshd


✅ Task 2.4: Kill a process
✅ Create a Dummy Process
sleep 1000 &

This will run sleep in the background for 1000 seconds.
It will return a Process ID (PID). Your PID may be different


kill -9 1011

📌 Be careful—only kill rogue or non-critical processes.

✅ Task 2.5: View memory performance

vmstat

Expected Output:

procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 524288  10240 204800    0    0     0     1   10   20  5  2 93  0  0

You notice your Linux machine is slow. You suspect:
High CPU usage
Low memory
Too much disk I/O
Run vmstat with a delay

vmstat 1 5

This gives 5 samples at 1-second intervals.

Pro Tip: Monitor in real-time with watch
watch -n 1 vmstat 1 1

This keeps refreshing every second like a dashboard.

Let's safely simulate high CPU and memory usage on your Linux machine, and observe it using vmstat.
🔁 Step-by-Step Simulation

🔧 1. Open 2 Terminals (or use tmux/screen)
One terminal will simulate load
The other will monitor with vmstat



⚙️ Terminal 1: Simulate High CPU Usage
Use the yes command — it prints continuously, consuming CPU.

yes > /dev/null &
yes > /dev/null &
yes > /dev/null &
yes > /dev/null &

This will spawn 4 CPU-intensive processes (safe and easily stoppable).
✅ Each yes uses ~100% of 1 core — on a 4-core machine, CPU should hit 100%.

⚙️ Terminal 2: Monitor with vmstat
vmstat 1 10

Watch for these changes:
r: Increases (CPU demand)
us: User CPU % increases
id: Idle drops close to 0%
wa: Should stay low (since no disk I/O)



🧠 Sample Output (under CPU stress):

procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 4  0      0 204800  10000 200000    0    0     0     0  200  400 99  0  1  0  0
 4  0      0 204000  10000 200500    0    0     0     0  210  420 98  1  1  0  0

r = 4: Four processes waiting
us = 98-99: CPU is heavily used by user processes
id = 1: Almost no idle time



💣 Stop the CPU Load
Kill the yes processes:
killall yes

Or manually with:
ps aux | grep yes
kill <PID>


🚀 BONUS: Simulate High Memory Usage
Create a memory-hungry Python process:
python3 -c "a = ['X' * 1024 * 1024] * 500" &

This allocates about 500 MB.
Monitor with:
vmstat 1 10
free drops
si/so might rise if swap is used



Let me know if you’d like to simulate disk I/O stress or create a small monitoring script to run vmstat with logs.





📦 Part 3: Package Management
✅ Task 3.1: Update package index

sudo apt update


✅ Task 3.2: Install NGINX

sudo apt install nginx

📌 Use curl localhost to test if it's running.

✅ Task 3.3: Remove NGINX

sudo apt remove nginx


✅ Task 3.4: List all installed packages

dpkg -l

📌 Helps in inventory management and auditing.

🔧 Part 4: Service Management
✅ Task 4.1: Start a service

sudo systemctl start nginx


✅ Task 4.2: Stop a service

sudo systemctl stop nginx


✅ Task 4.3: Restart a service (e.g., Apache)

sudo systemctl restart apache2


✅ Task 4.4: Reload a service

sudo systemctl reload nginx


✅ Task 4.5: Enable a service on boot

sudo systemctl enable apache2


✅ Task 4.6: Disable a service

sudo systemctl disable apache2


✅ Task 4.7: Check service status

sudo systemctl status docker

Expected Output (Example):

● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled)
     Active: active (running) since ...


✅ Task 4.8: List all active services

systemctl list-units --type=service




=======================================================================


