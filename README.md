# Linux Fundamentals - Part 1: Basics

## Introduction
This document covers fundamental concepts of Linux, including the kernel, file system, process management, shell scripting, and user management. It also provides practical terminal commands for hands-on learning.

## Kernel
The kernel is the core component of an operating system, responsible for managing hardware and software resources. It facilitates interactions between components, allocates system resources, and manages memory and peripheral devices.

### Types of Kernels
1. **Monolithic Kernel** - All OS services run in the kernel space.   
![image](https://github.com/user-attachments/assets/f2801c9f-4df5-4600-a857-b0f245f23b08)


2. **Microkernel** - OS services run in user space, reducing kernel complexity.
![image](https://github.com/user-attachments/assets/41771d0f-0875-41b5-862d-03af9d5374a5)


3. **Hybrid Kernel** - A mix of monolithic and microkernel, balancing efficiency and modularity.
![image](https://github.com/user-attachments/assets/115b9c14-ffd4-4a99-9457-efecce63341c)



### Kernel Commands
- `uname -r` - Display kernel version.
- `dmesg | less` - View system boot messages.
- `uptime` - Show system uptime.
- `cat /proc/version` - View kernel version and compilation details.

## RAM (Random Access Memory)
RAM stores program instructions and data temporarily. The kernel manages memory allocation to processes.

### Memory Management Commands
- `free -h` - Display memory usage.
- `vmstat` - Show system performance metrics.
- `top` or `htop` - Monitor real-time resource usage.
- `cat /proc/meminfo` - Show detailed memory statistics.

## Shell
The shell is an interface for users to interact with the Linux system through commands.

### Types of Shells
- **Bash (Bourne Again Shell)** - Default in most Linux distributions ($ prompt).
- **Bourne Shell (sh)** - The original Unix shell.
- **C Shell (csh)** - Syntax similar to C programming, preferred by some administrators (% prompt).

### Shell Commands
- `echo $SHELL` - Check the current shell.
- `chsh -s /bin/bash` - Change default shell to Bash.
- `history` - Show command history.
- `alias ll='ls -la'` - Create a shortcut for commands.

## Linux File System Hierarchy (FHS)
The File System Hierarchy Standard (FHS) defines directory structures in Linux.

### Key Directories
- **/bin** - Essential user commands.
- **/boot** - Boot-related files.
- **/dev** - Device files.
- **/etc** - Configuration files.
- **/home** - User directories.
- **/lib** - Shared system libraries.
- **/media** - Mount point for removable media.
- **/mnt** - Temporary mount point.
- **/opt** - Optional software packages.
- **/root** - Home directory for root.
- **/sbin** - System administration utilities.
- **/srv** - Data served by the system.
- **/tmp** - Temporary files.
- **/usr** - User applications and libraries.
- **/var** - Logs, cache, and spool files.

### File System Commands
- `ls -l` - List files with details.
- `pwd` - Show current directory.
- `cd /path` - Change directory.
- `df -h` - Show disk space usage.
- `du -sh directory/` - Show directory size.

## Linux File Types
- **Regular files (-)** - Text, scripts, binary files.
- **Directory (d)** - Contains files and subdirectories.
- **Character device files (c)** - Interfaces for hardware.
- **Block device files (b)** - Storage devices like hard drives.
- **Socket files (s)** - Local inter-process communication.
- **Named pipes (p)** - FIFO communication between processes.
- **Symbolic links (l)** - Shortcuts to files or directories.

## Control Operators
- **Semicolon (;)** - Runs multiple commands sequentially.
- **Ampersand (&)** - Executes a command in the background.
- **Double ampersand (&&)** - Runs the second command only if the first succeeds.
- **Hash (#)** - Commenting in scripts.

### Practical Examples
- `mkdir test; cd test` - Create and navigate to a directory.
- `echo "hello" > file.txt &` - Write to a file in the background.
- `ls && echo "Listed successfully"` - List files only if the command succeeds.

## I/O Redirection
- Redirects command input/output to/from files.
- Example: `echo "text" >> file.txt` (appends text to a file).

### Redirection Commands
- `cat file.txt > newfile.txt` - Copy file contents.
- `sort < file.txt > sorted.txt` - Sort file and save output.
- `grep error logfile.txt >> errors.txt` - Append errors to a file.

## Filters and Pipes
- **Filters** - Process data from another command (e.g., `grep`).
- **Pipes (|)** - Pass output of one command to another.
# **🔍 `grep` Command in Linux - Explained with Examples**  

The `grep` command is used to **search for a specific pattern** (word, phrase, or regex) in a file or multiple files. It scans the text and prints lines that match the pattern.  

📌 **Syntax:**  
```bash
grep [OPTIONS] PATTERN FILE
```
- **`PATTERN`** → The text or regex to search for.  
- **`FILE`** → The file(s) in which to search.  
- **`OPTIONS`** → Modify `grep` behavior (like case-insensitive search, whole word match, etc.).

---

## **1️⃣ Basic `grep` Usage**
### **🔹 Search for a word in a file**
```bash
grep "error" logfile.txt
```
🔹 **Output:** *(Shows all lines containing "error")*  
```
[ERROR] Failed to connect to server
[ERROR] File not found
```
📌 **Case-sensitive**: It will only match lowercase `error` (not `Error` or `ERROR`).

---

## **2️⃣ Case-Insensitive Search (`-i`)**
🔹 **Example:**  
```bash
grep -i "error" logfile.txt
```
✔ Matches **`error`**, **`ERROR`**, **`Error`**, etc.

---

## **3️⃣ Search in Multiple Files**
```bash
grep "404" access.log error.log
```
🔹 **Output Example:**
```
access.log: Page not found - 404 error
error.log: HTTP 404 - Not Found
```
📌 **Shows the file name before the matching line.**

---

## **4️⃣ Display Only Matching Lines (`-o`)**
```bash
grep -o "404" access.log
```
✔ Prints only **"404"**, not the entire line.

---

## **5️⃣ Count Matches (`-c`)**
```bash
grep -c "failed" system.log
```
✔ Outputs **the number of times** "failed" appears.

---

## **6️⃣ Show Line Numbers (`-n`)**
```bash
grep -n "user" users.txt
```
✔ Prints **line numbers** where "user" is found.

🔹 **Example Output:**
```
3: New user created
7: User login failed
```
*(Matches at lines 3 and 7.)*

---

## **7️⃣ Match Whole Words (`-w`)**
```bash
grep -w "is" example.txt
```
✔ Matches **"is"** but NOT **"this"** or **"inside"**.

---

## **8️⃣ Invert Match (`-v`)**
```bash
grep -v "ERROR" logfile.txt
```
✔ Shows **all lines that DO NOT contain "ERROR".**

---

## **9️⃣ Recursive Search in Directories (`-r`)**
```bash
grep -r "password" /etc/
```
✔ Searches **inside all files** in `/etc/` for "password".

---

## **🔍 Advanced: Using `grep` with Regular Expressions**
### **Match Any Character (`.`)**
```bash
grep "c.t" words.txt
```
✔ Matches **"cat", "cut", "cot"**, etc.

### **Match Beginning of Line (`^`)**
```bash
grep "^root" /etc/passwd
```
✔ Matches lines that **start** with "root".

### **Match End of Line (`$`)**
```bash
grep "error$" logfile.txt
```
✔ Matches lines that **end** with "error".

---

## **📌 Combining `grep` with Other Commands**
### **1️⃣ Search Inside Command Output**
```bash
ps aux | grep "chrome"
```
✔ Finds **running processes** containing "chrome".

### **2️⃣ Filter Logs in Real-Time**
```bash
tail -f /var/log/syslog | grep "failed"
```
✔ Shows **only lines with "failed"** in a live log.

---

## **📝 Summary Table**
| Option | Function | Example |
|---------|-------------|-----------------|
| `-i` | Case-insensitive search | `grep -i "error" file.txt` |
| `-o` | Print only matching words | `grep -o "404" access.log` |
| `-c` | Count occurrences | `grep -c "failed" system.log` |
| `-n` | Show line numbers | `grep -n "user" users.txt` |
| `-w` | Match whole word | `grep -w "is" example.txt` |
| `-v` | Show lines that **don't** match | `grep -v "ERROR" logfile.txt` |
| `-r` | Recursive search in directories | `grep -r "password" /etc/` |

---

## **✅ Conclusion**
- `grep` is a **powerful** text-search tool.  
- It can **search inside files**, **count occurrences**, **find patterns**, and **filter logs**.  
- Supports **regular expressions** for **advanced searches**.  

### Practical Examples
- `ls | grep txt` - Lists only files containing "txt".
- `ps aux | sort -k3nr | head -5` - Show top 5 CPU-consuming processes.
- `find . -type f | wc -l` - Count all files in the current directory.

## Process Management
- **Foreground process** - Runs in terminal, requires user input.
- **Background process** - Runs independently.

### Process Commands
- `ps` - Lists running processes.
- `top` - Displays real-time process activity.
- `kill -9 PID` - Force kill a process.
- `jobs` - Show background jobs.
- `fg %1` - Bring job 1 to foreground.
- `nohup command &` - Run a process that ignores hang-ups.

## Scripting Introduction
A shell script is a series of commands written in a file to automate tasks.

### Basic Script Example
```sh
#!/bin/bash
echo "Hello, Linux!"
```

### Executing a Script
- `chmod +x script.sh` - Make script executable.
- `./script.sh` - Run script.

## User and Group Management
### Types of Accounts
- **Root User** - Superuser with full system access.
- **Service Accounts** - Used by system services.
- **User Accounts** - Regular users with restricted access.
- **Groups** - Logical collection of users for permission management.

### Key Files for User Management
- **/etc/passwd** - User account information.
- **/etc/shadow** - Encrypted passwords.
- **/etc/group** - Group information.
- **/etc/gshadow** - Secure group account information.

### Managing Users and Groups
- `useradd username` - Add a user.
- `passwd username` - Set user password.
- `usermod -aG groupname username` - Add user to a group.
- `id username` - Show user ID and group info.
- `groupadd groupname` - Add a new group.
- `groupdel groupname` - Delete a group.

## Conclusion
This document provides an overview of fundamental Linux concepts, including the kernel, file systems, process management, shell scripting, and user management. It includes essential terminal commands for practice, forming a strong foundation for Linux administration and usage.

