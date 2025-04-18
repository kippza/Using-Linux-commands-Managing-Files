# Using-Linux-commands-Managing-Files


---

# 🔐 File Permissions in Linux

## 📘 Project Description

In this project, I worked as a security professional responsible for auditing file permissions in a research team's working directory on a Linux system. The goal was to ensure that only authorized users had appropriate access to sensitive files and directories. I used Linux commands to identify and correct permission issues, aligning the system's configuration with organizational security policies.

---

## 📁 File and Directory Permission Details

### 🔍 Check File and Directory Permissions

**Command:**
```bash
ls -la /home/researcher2/projects
```

This command lists all files (including hidden files) in long format, displaying permission strings, ownership, and timestamps.

**Output Example:**
```
-rw-rw-rw- 1 researcher2 research 1234 Apr 17 10:00 project_k.txt
-rw-r----- 1 researcher2 research 2345 Apr 17 10:00 project_m.txt
-rw-rw-r-- 1 researcher2 research 3456 Apr 17 10:00 project_r.txt
-rw-rw-r-- 1 researcher2 research 4567 Apr 17 10:00 project_t.txt
-rw--w---- 1 researcher2 research 5678 Apr 17 10:00 .project_x.txt
drwx--x--- 1 researcher2 research    0 Apr 17 10:00 drafts
```

---

## 🧩 Understanding Permissions

### 🔠 Example Breakdown

**Example:**  
```
-rw-rw-rw- (for project_k.txt)
```

**Explanation:**

- `-`: Regular file  
- `rw-`: User has read and write access  
- `rw-`: Group has read and write access  
- `rw-`: Others have read and write access ❌ (violation!)

According to policy, *others should never have write access*.

---

## 🔧 Fixing File Permissions

### 🚫 Remove Write Access for Others on `project_k.txt`

**Command:**
```bash
chmod o-w /home/researcher2/projects/project_k.txt
```

**Result:**
```
-rw-rw-r-- 1 researcher2 research 1234 Apr 17 10:00 project_k.txt
```

✅ *Write access for "others" removed.*

---

## 👻 Secure Hidden File: `.project_x.txt`

### 📋 Policy:  
- User: ✅ read  
- Group: ✅ read  
- Others: ❌ no access  
- No one should have write access

**Command:**
```bash
chmod 440 /home/researcher2/projects/.project_x.txt
```

**Result:**
```
-r--r----- 1 researcher2 research 5678 Apr 17 10:00 .project_x.txt
```

✅ *Hidden file is now read-only for user and group.*

---

## 📂 Secure Directory Access: `drafts`

### 📋 Policy:  
Only the user `researcher2` should have full access.

**Command:**
```bash
chmod 700 /home/researcher2/projects/drafts
```

**Result:**
```
drwx------ 1 researcher2 research 0 Apr 17 10:00 drafts
```

✅ *Access restricted to the owner only.*

---

## 📝 Summary

This project focused on auditing and correcting file and directory permissions in a Linux environment. Using `ls -la` to check current states and `chmod` to apply changes, I ensured that:

- No unauthorized write access is granted to "others"
- Hidden files like `.project_x.txt` are secure
- Directories like `drafts` are only accessible to their owner

These actions reinforce the organization’s least-privilege policy and help protect sensitive research data.

---


