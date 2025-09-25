# Day 11 - User and Group Management in Linux

## Summary
Today I focused on **Linux user and group management**. These skills are essential for securely managing servers in Cloud and DevOps environments.

---

## Topics Covered

### Linux File System Hierarchy
- Learned the structure of `/`, `/home`, `/etc`, `/var`, `/usr`, and other directories.  
- Understood where system configs, logs, and binaries are stored.  

### Navigation
- Practiced **relative paths** (e.g., `cd ../dir`)  
- Practiced **absolute paths** (e.g., `cd /home/user/dir`)  

### User & Group Management
- `sudo adduser username` → Create a new user  
- `sudo groupadd groupname` → Create a new group  
- `sudo usermod -aG groupname username` → Add user to group  
- `id username` → Check user group membership  

### Sudo & Custom Groups
- `sudo usermod -aG sudo username` → Grant sudo privileges  
- Created and assigned users to **custom groups** for role-based access.  

### Permissions & Verification
- `ls -l` → Check file permissions  
- Verified group assignments and understood how permissions affect collaboration and security.  

---

## Key Learnings
✅ Understood Linux file system hierarchy  
✅ Navigated with relative and absolute paths  
✅ Created and managed users and groups  
✅ Assigned users to sudo and custom groups  
✅ Verified permissions and learned why groups matter  

---

## Takeaway
User and group management is **the backbone of Linux security**. As a DevOps engineer, controlling access ensures safe and collaborative environments in **cloud servers and production systems**.
