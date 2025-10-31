#### Date: 31st October 2025
# Linux Refresher for DevOps

## 1. Introduction to Linux
Linux is the backbone of the internet and DevOps. Most servers, containers, 
and cloud infrastructures run on Linux distributions like Ubuntu, CentOS, 
Debian, and RHEL. Understanding Linux is crucial for managing 
infrastructure and deploying applications.

## 2. The Linux File System Hierarchy
- `/`: The root directory.
- `/bin` & `/usr/bin`: Executable binaries for all users.
- `/etc`: System configuration files.
- `/home`: User home directories.
- `/root`: Home directory for the root user.
- `/var`: Variable files like logs (`/var/log`) and mail.
- `/tmp`: Temporary files (deleted on reboot).
- `/proc`: Virtual filesystem containing process information.

## 3. Essential Command Line Interface (CLI) Commands

### File and Directory Operations
- `ls -lah`: List all files with detailed info and human-readable sizes.
- `cd <dir>`: Change directory.
- `pwd`: Print working directory.
- `mkdir -p <dir>`: Create directories (and parents if missing).
- `cp -r <src> <dest>`: Copy files/directories recursively.
- `mv <src> <dest>`: Move or rename files/directories.
- `rm -rf <file/dir>`: Remove files or directories forcefully (Caution!).
- `touch <file>`: Create an empty file.

### Text Processing
- `cat <file>`: Display file content.
- `grep "pattern" <file>`: Search for text inside files.
- `head -n 10 <file>`: Show first 10 lines.
- `tail -f <file>`: Follow log files in real-time.
- `sed`: Stream editor for basic text transformation.
- `awk`: Powerful pattern scanning and processing language.

## 4. Permissions and Ownership
Linux is a multi-user system. Permissions are defined for User (u), 
Group (g), and Others (o).
- `r` (Read: 4), `w` (Write: 2), `x` (Execute: 1).
- `chmod 755 <file>`: Read/write/execute for owner, read/execute for others.
- `chown <user>:<group> <file>`: Change owner and group.

## 5. Process Management
- `top` or `htop`: Monitor system resources and running processes.
- `ps aux`: List all running processes.
- `kill -9 <PID>`: Forcefully terminate a process.
- `systemctl start/stop/status <service>`: Manage systemd services.

## 6. Networking Basics
- `ip addr`: Show IP addresses and network interfaces.
- `ping <host>`: Check connectivity to a host.
- `netstat -tuln`: List listening ports and connections.
- `curl -v <URL>`: Transfer data and see verbose output.
- `ssh <user>@<host>`: Securely connect to a remote machine.

## 7. Package Management
Different distributions use different package managers:
- **Ubuntu/Debian:** `apt update`, `apt install <pkg>`.
- **CentOS/RHEL:** `yum` or `dnf install <pkg>`.

## 8. Shell and Scripting
The shell (typically Bash or Zsh) is the interface to the kernel. 
Scripting allows automation of repetitive tasks.
- `#!/bin/bash`: The shebang line.
- Variables: `NAME="Devops"`.
- Loops and Conditionals: Fundamental logic in scripts.

## 9. Conclusion
Linux proficiency is not optional for a DevOps engineer. It provides the 
flexibility and control needed to automate deployments, troubleshoot 
issues, and optimize server performance.

---
*End of Notes*
