# Month 1: Linux Fundamentals & Cybersecurity Foundations

**Student:** Maxwell John  
**Program:** GoMyCode Cybersecurity Bootcamp & Cisco Networking Academy  
**Objective:** Building a strong foundation in Linux system administration to transition into a Junior Cybersecurity Analyst role.

---

## 📌 Executive Summary
During my first month of intensive cybersecurity training, I built a virtual home lab and developed a strong foundation in Linux system administration. I progressed from basic command-line navigation to managing system resources, configuring background services, and hardening file permissions. I also completed the introductory Cisco cybersecurity module, establishing a theoretical understanding of modern security principles.

## 🛠️ Home Lab Configuration
*   **Host OS:** Windows 10 (8GB RAM, Intel Celeron)
*   **Hypervisor:** Oracle VirtualBox
*   **Target Environment:** Kali Linux (2GB RAM) & Ubuntu WSL
*   **Communication & Version Control:** Discord (cohort collaboration) & GitHub (portfolio documentation)

---

## 🧠 Core Competencies & Commands Mastered

### 1. The Linux Filesystem (Directory Tree)
Understanding the Linux directory tree is crucial for navigation and system administration. I learned the purpose of the top-level directories:
*   **`/` (Root Directory):** The top of the entire filesystem. Everything starts here.
*   **`/home`:** The residential wing. Contains personal folders for regular users (e.g., `/home/kali`).
*   **`/root`:** The admin's private penthouse. Not inside `/home`. Only the root user can access it.
*   **`/etc`:** City Hall. Stores system configuration files (e.g., `/etc/passwd`, `/etc/shadow`, `/etc/group`).
*   **`/var/log`:** The Security Office. Stores system logs and records of activity.
*   **`/bin` & `/usr/bin`:** The public toolshed. Contains basic programs and user binaries (`ls`, `cp`, `grep`).
*   **`/tmp`:** The public scratchpad. Temporary files that are cleared on reboot.
*   **`/dev`:** Doors to hardware (hard drives, USB, keyboard).

### 2. Linux Navigation & File Management
*   Navigated the directory tree using `pwd` (Print Working Directory), `cd` (Change Directory), and `ls -la` (List All).
*   Differentiated between Absolute Paths (`/home/kali`) and Relative Paths (`cd ..`).
*   Managed files and directories using `touch` (create file), `mkdir` (make directory), `cp` (copy), `mv` (move/rename), and `rm` / `rm -r` (delete).

### 3. Search, Filter & Text Processing
*   Utilized `find` to locate files by name and `grep` to search for specific text patterns inside files.
*   Chained commands using pipes (`|`) to filter and count results (e.g., `grep "Failed" auth.log | wc -l`).
*   Managed output using redirection operators: `>` (overwrite file) and `>>` (append to file).
*   Used wildcards (`*`) to match multiple files at once (e.g., `file ./-file*`).

### 4. User & Group Management
*   Created and deleted users with `adduser` and `deluser`. 
*   Managed group memberships using `groupadd` and `usermod -aG` (Append to Group).
*   **Sudoers VIP List:** Learned that regular users cannot use `sudo` until they are added to the `sudo` group (which is defined in `/etc/sudoers`).
*   Changed file ownership using `chown` (requires `sudo`).
*   Enforced the Principle of Least Privilege by using `sudo` for administrative tasks instead of logging in as root.

### 5. File Permissions & Security (Octal & Symbolic)
*   Mastered the Octal (Numerical) system: Read (4), Write (2), Execute (1).
*   Applied permissions using **Numerical** method (`chmod 755` for scripts, `chmod 644` for files, `chmod 600` for private documents).
*   Applied permissions using **Symbolic** method (`chmod u+x`, `chmod o-r`, `chmod g+rw`).
*   Understood Directory vs. File permissions: `x` is needed to `cd` into a folder, `r` is needed to `ls` its contents, and `w` is needed to create/delete inside it.

### 6. Package & System Management
*   Managed software securely using the `apt` package manager (`update`, `upgrade`, `install`, `autoremove`, `clean`).
*   Successfully performed a major system upgrade of **1,505 packages** on a low-spec VM.
*   Managed background system units (services) using `systemctl` (`status`, `start`, `stop`, `enable`).
*   Monitored system resources to prevent crashes using `df -h` (disk free) and `free -h` (memory free).

### 7. Web Server Concepts
*   Installed Apache locally to understand the Client-Server model.
*   Verified that Apache listens on **Port 80** by loading the default "It works!" page via `localhost` in Firefox.

---

## 🎮 OverTheWire: Bandit Wargame (Levels 0 - 11)
To reinforce my Linux skills, I completed the first 12 levels of the Bandit wargame, which taught me practical problem-solving in a live SSH environment:
*   **SSH:** Learned to connect to remote servers securely using `ssh user@host -p 2220`.
*   **Special Characters:** Handled files with spaces (using quotes or Tab completion) and files starting with dashes (using `./` or `--`).
*   **Hidden Files:** Used `ls -la` to find hidden files.
*   **File Types:** Used the `file` command to identify ASCII text vs. binary data.
*   **Advanced Search:** Used `find` with specific filters (`-size`, `-user`, `-group`, `! -executable`) to locate exact files in massive directories.
*   **Text Processing:** Used `sort`, `uniq -u`, `strings`, `base64 -d`, and `tr` to decode and filter data.

## 🛡️ Cybersecurity Foundations (Cisco Networking Academy)
*   **Completed:** Module 1 - Introduction to Cybersecurity.
*   **Key Concepts:** The CIA Triad (Confidentiality, Integrity, Availability), malware types (viruses, worms, trojans), social engineering, and the importance of security policies.

---

## 🛠️ Technical Troubleshooting Log
*Documenting resolved technical challenges to demonstrate analytical and problem-solving skills.*

*   **Issue 1: "Directory Not Empty" Error**
    *   *Problem:* Attempted to delete a folder using `rmdir`, but received an error.
    *   *Resolution:* Learned that `rmdir` only works on empty directories. Successfully deleted the folder using `rm -r`, which recursively removes contents.
    *   *Lesson:* Linux protects against accidental data loss by requiring explicit recursive flags.

*   **Issue 2: Process Blocking User Deletion (Stubborn User)**
    *   *Problem:* Unable to delete a test user (`bob`) due to the error: "user is currently used by process 55350."
    *   *Resolution:* Attempted to find and kill the process (`ps -u bob`, `pkill -9 -u bob`). The process was in an uninterruptible (zombie) state. Ultimately resolved by re-running `sudo deluser --remove-home bob`, forcing the system to clean up the orphaned process.
    *   *Lesson:* Linux handles process cleanup gracefully if you let the system utilities manage the task. 

*   **Issue 3: "Permission Denied" on Directory Creation**
    *   *Problem:* Received "Permission denied" when creating a folder inside `/home`.
    *   *Resolution:* Realized that regular users cannot write to the parent directory. Used `cd ~` to navigate to the personal home directory (`/home/kali`) before creating folders.
    *   *Lesson:* Always verify your current location with `pwd` before creating or modifying files.

*   **Issue 4: Command Syntax Errors (`chmod` & `mv`)**
    *   *Problem:* Encountered syntax errors when combining permissions (`chmod o+x o+w file`) and forgetting the action verb for moves (`renamed_copy.txt folder/`).
    *   *Resolution:* Learned that `chmod` requires combined flags (`chmod o+wx`) and `mv` requires the explicit `mv` command prefix.
    *   *Lesson:* Linux commands are strict about syntax; every argument must be explicitly declared.

*   **Issue 5: Terminal Typo and Unclosed Quotes**
    *   *Problem:* Received a `dquote>` prompt and got stuck while trying to write a log file using `echo`.
    *   *Resolution:* Realized I forgot the closing quotation mark (`"`). Pressed `Ctrl + C` to cancel, deleted the corrupted file, and re-ran the command with correct syntax (`echo -e "text\n" > file.log`).
    *   *Lesson:* Always close your quotes. `Ctrl + C` is your best friend when a command gets stuck.

---

## 📸 Verification & Proof of Work
*(Going through the lab again to take fresh screenshots. Will drop them below.)*

**1. Linux Navigation & File Management:**


**2. User Management & Groups:**
*[Screenshot of `adduser`, `id`, `groupadd`]*

**3. Octal & Symbolic Permissions:**
*[Screenshot of `chmod 755` or `chmod u+x`]*

**4. Package Management & System Upgrades:**
*[Screenshot of `df -h` or `htop`]*

**5. Systemctl Services:**
*[Screenshot of `systemctl status ssh`]*

**6. Apache Web Server:**
*[Screenshot of Firefox "It works!" page]*

**7. OverTheWire Bandit Progress:**
*[Screenshot of a solved Bandit level]*

---

## 🎯 Next Steps (Month 2)
*   Transition into Networking Fundamentals (IP addressing, Subnets, VLANs).
*   Set up Windows Server 2016 and Windows 10 in VirtualBox to build an Active Directory lab.
*   Master remote administration tools (SSH keys, SCP, Rsync).
*   Learn log analysis and real-time monitoring (`tail -f`, `journalctl`).
