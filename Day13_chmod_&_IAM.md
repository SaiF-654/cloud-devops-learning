# Day 13 - Mise Academy  

## Topic: File & Cloud Access Control with chmod and IAM  

### Objectives
- Change file permissions using `chmod`  
- Create IAM users and assign roles  
- Create a group and assign users to it  
- Sign in as IAM user  
- Verify read-only EC2 access  

---

### 🔹 Linux Practice with `chmod`
We experimented with different permission sets:

```bash
# Create a file
touch backup.sh

# Add content
echo "Currently, I am learning IAM user creation" > backup.sh

# View file permissions
ls -l

# Change permissions
chmod 755 backup.sh
chmod 777 backup.sh
chmod 644 backup.sh
chmod +x backup.sh
