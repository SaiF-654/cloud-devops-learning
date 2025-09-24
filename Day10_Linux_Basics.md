# Day 10 - Linux Basics for Cloud & DevOps

## Summary
Today I practiced essential Linux commands that every Cloud & DevOps engineer should know. These commands help in system navigation, file management, monitoring, backups, permissions, and system control.

---

## Commands Covered

### Navigation
- `pwd` → Print working directory  
- `cd`, `cd~` → Change directory  

### File & Directory Management
- `ls -l`, `ls -al` → List files with details  
- `cp` → Copy files  
- `mv` → Move/rename files  
- `touch` → Create new empty files  
- `mkdir` → Create directories  
- `rm`, `rm -r` → Remove files/directories  

### Editing Files
- `vim filename` → Edit files with Vim  
- `nano filename` → Edit files with Nano  

### Logs & Monitoring
- `journalctl -f` → View live logs  
- `less /var/log/syslog` → Scroll through logs  
- `head -n 10 /var/log/syslog` → View first 10 lines  
- `tail -n 10 /var/log/syslog` → View last 10 lines  

### System & User
- `whoami` → Show current user  
- `sudo -i` → Switch to root user  
- `sudo reboot` → Reboot system  
- `sudo shutdown now` → Shutdown system immediately  

---

## Key Learnings
✅ Check system directories  
✅ Monitor log files  
✅ Create backups  
✅ Edit configuration files  
✅ Handle user permissions  
✅ Safely shut down or reboot the server  

---

## Takeaway
Linux is the **foundation of cloud servers and DevOps tools**. Mastering these basics helps in managing real-world cloud infrastructure effectively.
