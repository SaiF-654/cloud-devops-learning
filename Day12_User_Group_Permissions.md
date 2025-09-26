# Day 12 - Configuring User and Group Permissions in Linux

## Summary
Today's focus was on **user, group, and file permission management** in Linux. These skills are critical for **secure system administration** and for maintaining compliance in **enterprise cloud projects**.

---

## Topics Covered

### User Management
- `sudo adduser username` → Create a new user  
- `passwd username` → Assign password to a user  
- `sudo usermod -aG sudo username` → Grant sudo access  

### Group Management
- `sudo groupadd groupname` → Create a group  
- `sudo usermod -aG groupname username` → Add user to group  
- `groups username` → Verify user’s group memberships  

### File Ownership & Permissions
- `ls -l` → List file permissions and ownership  
- `sudo chown user:group filename` → Change file ownership  
- `chmod 644 filename` → Set read/write permissions  
- `chmod 755 script.sh` → Set execute permissions for scripts  

### Real-Time Testing
- Simulated **enterprise setups** with multiple users and groups.  
- Practiced granting and restricting access to sensitive files.  

---

## Key Takeaways
✅ Created and managed users effectively  
✅ Practiced group creation and assignment  
✅ Configured secure file ownership and permissions  
✅ Understood importance of least privilege & RBAC  
✅ Applied concepts to **real-world cloud security scenarios**  

---

## Conclusion
Managing users, groups, and permissions is **vital for security in Linux servers**. These practices help ensure **data protection, compliance (GDPR, SOC 2, HIPAA)**, and smooth collaboration in **DevOps & cloud environments**.
