# Linux System Administration

This will covers:

* Package Management
* APT, Snap & DPKG
* Process Management
* Process Lifecycle
* Linux Namespaces & cgroups
* Permission Commands
* Text & Search Commands
* Process Management Commands
* Network Commands

---

# Table of Contents

* [1. Package Management](#1-package-management)

  * [APT](#apt)
  * [Snap](#snap)
  * [DPKG](#dpkg)
  * [`apt update`](#apt-update-vs-apt-upgrade)[ vs ](#apt-update-vs-apt-upgrade)[`apt upgrade`](#apt-update-vs-apt-upgrade)
* [2. Process Management](#2-process-management)

  * [Process](#process)
  * [Process Lifecycle](#process-lifecycle)
  * [Process States](#process-states)
  * [Process IDs](#process-ids)
  * [Namespaces](#namespaces)
  * [cgroups](#cgroups)
* [3. Permission Commands](#3-permission-commands)

  * [`ls -ltra`](#ls--ltra)
  * [`chmod`](#chmod)
  * [`chown`](#chown)
  * [`chgrp`](#chgrp)
* [4. Text & Search Commands](#4-text--search-commands)

  * [`cat`](#cat)
  * [`less`](#less)
  * [`head`](#head)
  * [`tail`](#tail)
  * [`grep`](#grep)
  * [`find`](#find)
  * [`wc`](#wc)
  * [`sort`](#sort)
  * [`uniq`](#uniq)
  * [`cut`](#cut)
* [5. Process Management Commands](#5-process-management-commands)

  * [`ps`](#ps)
  * [`top`](#top)
  * [`htop`](#htop)
  * [`kill`](#kill)
  * [`pkill`](#pkill)
  * [`pgrep`](#pgrep)
  * [`jobs`](#jobs)
  * [`fg`](#fg)
  * [`bg`](#bg)
* [6. Network Commands](#6-network-commands)

  * [`ip`](#ip)
  * [`ping`](#ping)
  * [`ss`](#ss)
  * [`curl`](#curl)
  * [`wget`](#wget)
  * [`hostname`](#hostname)
  * [`dig`](#dig)
  * [`nslookup`](#nslookup)
  * [`traceroute`](#traceroute)

---

# 1. Package Management

Package management is used to:

* Install software
* Remove software
* Update software
* Upgrade software
* Search packages
* Check installed packages
* Manage dependencies

Ubuntu primarily uses:

```text
APT
SNAP
DPKG
```

---

## APT

**APT (Advanced Package Tool)** is the high-level package management tool commonly used in Ubuntu.

APT works with configured software repositories and manages package dependencies.

### Update Package Information

```bash
sudo apt update
```

This downloads the latest package information from configured repositories.

It does **not** upgrade the installed packages.

Think of it as:

```text
Repository
    ↓
Latest Package Information
    ↓
Local Package Index
```

### Upgrade Installed Packages

```bash
sudo apt upgrade
```

This installs newer versions of installed packages when available.

### Common Workflow

```bash
sudo apt update
sudo apt upgrade
```

Remember:

```text
apt update
    ↓
Update package information

apt upgrade
    ↓
Upgrade installed packages
```

---

## Install a Package

```bash
sudo apt install package-name
```

Example:

```bash
sudo apt install nginx
```

APT automatically handles package dependencies.

---

## Remove a Package

```bash
sudo apt remove nginx
```

This removes the package while generally leaving its configuration files.

To remove the package and its configuration files:

```bash
sudo apt purge nginx
```
---

## Search for a Package

```bash
apt search nginx
```

---

## Show Package Information

```bash
apt show nginx
```

---

## List Installed Packages

```bash
apt list --installed
```

---

## Remove Unused Dependencies

```bash
sudo apt autoremove
```

This removes packages that were automatically installed as dependencies and are no longer required.

---

# Snap

**Snap** is an application packaging and distribution system commonly available on Ubuntu.

Snap applications are distributed as **snap packages**.

### Search for a Snap

```bash
snap search package-name
```

### Install a Snap

```bash
sudo snap install package-name
```

Example:

```bash
sudo snap install code --classic
```

### List Installed Snaps

```bash
snap list
```

### Remove a Snap

```bash
sudo snap remove package-name
```

### Update Snaps

```bash
sudo snap refresh
```

### Show Snap Information

```bash
snap info package-name
```

---

# DPKG

**DPKG** is the low-level package management tool used by Debian-based distributions such as Ubuntu.

It works directly with `.deb` packages.

The relationship can be understood as:

```text
APT
 ↓
High-Level Package Management
 ↓
Dependency / Repository Management
 ↓
DPKG
 ↓
.deb Package Management
```

---

## Install a `.deb` Package

```bash
sudo dpkg -i package.deb
```

If dependencies are missing, repair them with:

```bash
sudo apt --fix-broken install
```

---

## Remove a Package

```bash
sudo dpkg -r package-name
```

---

## List Installed Packages

```bash
dpkg -l
```

---

## Search Installed Packages

```bash
dpkg -l | grep nginx
```

---

## Show Package Information

```bash
dpkg -s package-name
```

---

## Find Which Package Owns a File

```bash
dpkg -S /path/to/file
```

---

# APT vs Snap vs DPKG

| Tool   | Purpose                             | Package Type |
| ------ | ----------------------------------- | ------------ |
| `apt`  | High-level package management       | `.deb`       |
| `snap` | Application package management      | Snap         |
| `dpkg` | Low-level Debian package management | `.deb`       |

---

# 2. Process Management

A **process** is a running instance of a program.

For example:

```bash
python3 app.py
```

When the command starts executing, Linux creates a process.

```text
Program
   ↓
Execution
   ↓
Process
```

A process contains information such as:

* Process ID (PID)
* Parent Process ID (PPID)
* User
* Process state
* CPU usage
* Memory usage
* Open files
* Environment

---

## Process Lifecycle

A simplified process lifecycle:

```text
             fork()
Parent ───────────────→ Child
                          │
                          │ exec()
                          ↓
                       Program
                          │
                          ↓
                       Running
                          │
                        exit()
                          ↓
                       Zombie
                          │
                   Parent reaps it
                          ↓
                       Removed
```

A process can move through different states during its lifetime:

```text
Created
   ↓
Running
   ↓
Waiting / Sleeping
   ↓
Stopped
   ↓
Terminated
```

---

## Process States

Common Linux process states:

| State | Meaning               |
| ----- | --------------------- |
| `R`   | Running or runnable   |
| `S`   | Interruptible sleep   |
| `D`   | Uninterruptible sleep |
| `T`   | Stopped               |
| `Z`   | Zombie                |

You can view process states using:

```bash
ps aux
```

---

## Process IDs

Every running process has a **PID (Process ID)**.

Example:

```text
PID
1001
1002
1003
```

Linux also maintains a parent-child relationship between processes.

### PID

Identifies the current process.

### PPID

Identifies the parent process.

View them using:

```bash
ps -ef
```

Example:

```text
UID     PID   PPID   CMD
rahul   1200  1100   bash
rahul   1250  1200   nginx
```

Here:

```text
bash
  ↓
nginx
```

---

## Namespaces

**Linux namespaces** provide isolation for processes.

Namespaces allow processes to have isolated views of specific system resources.

Common namespace types:

```text
PID
Network
Mount
UTS
IPC
User
Cgroup
```

### PID Namespace

A PID namespace provides a process with an isolated view of process IDs.

For example, a process inside a container may see:

```text
PID 1
PID 2
PID 3
```

while the host system has many more processes.

Namespaces are one of the fundamental technologies used to isolate containers.

---

## cgroups

**cgroups (Control Groups)** are used to organize processes and control/account for their resource usage.

They can manage resources such as:

```text
CPU
Memory
I/O
PIDs
```

Conceptually:

```text
Application
    ↓
Processes
    ↓
cgroup
    ├── CPU control
    ├── Memory control
    ├── I/O control
    └── Process limit
```

### Namespace vs cgroup

A simple way to remember:

```text
Namespace
    ↓
"What can this process see?"
```

```text
cgroup
    ↓
"How many resources can this process use?"
```

Namespaces provide isolation, while cgroups provide resource control and accounting.

Both are fundamental Linux technologies used by container platforms.

---

# 3. Permission Commands

Linux permissions control access to files and directories.

There are three basic permissions:

```text
r → Read
w → Write
x → Execute
```

And three categories:

```text
u → User / Owner
g → Group
o → Others
```

---

## `ls -ltra`

To view detailed information about files and directories:

```bash
ls -ltra
```

Options:

```text
-l → Long listing format
-t → Sort by modification time
-r → Reverse the sorting order
-a → Show hidden files
```

Example:

```text
-rwxr-xr-- 1 rahul developers 1200 Aug 31 script.sh
```

Permission section:

```text
rwx | r-x | r--
 ↓     ↓     ↓
User  Group Others
```

---

## `chmod`

`chmod` is used to change file and directory permissions.

### Numeric Method

```bash
chmod 755 script.sh
```

Permission values:

```text
r = 4
w = 2
x = 1
```

Common permissions:

```text
644 = rw-r--r--
755 = rwxr-xr-x
700 = rwx------
600 = rw-------
```

### Symbolic Method

Add execute permission to owner:

```bash
chmod u+x script.sh
```

Add write permission to group:

```bash
chmod g+w file.txt
```

Remove write permission from others:

```bash
chmod o-w file.txt
```

Add execute permission to everyone:

```bash
chmod a+x script.sh
```

---

## `chown`

`chown` changes the ownership of a file or directory.

Change owner:

```bash
sudo chown rahul file.txt
```

Change owner and group:

```bash
sudo chown rahul:developers file.txt
```

---

## `chgrp`

`chgrp` changes the group ownership.

```bash
sudo chgrp developers file.txt
```

---

# 4. Text & Search Commands

Linux provides several commands for reading, processing, and searching text.

---

## `cat`

Display the contents of a file:

```bash
cat file.txt
```

---

## `less`

Read a file page by page:

```bash
less file.txt
```

Useful for large files and log files.

---

## `head`

Display the beginning of a file:

```bash
head file.txt
```

Display the first 20 lines:

```bash
head -n 20 file.txt
```

---

## `tail`

Display the end of a file:

```bash
tail file.txt
```

Display the last 20 lines:

```bash
tail -n 20 file.txt
```

Follow a log file in real time:

```bash
tail -f /var/log/syslog
```

---

## `grep`

Search for text inside files.

```bash
grep "error" logfile.txt
```

Case-insensitive search:

```bash
grep -i "error" logfile.txt
```

Recursive search:

```bash
grep -r "error" /var/log
```

Show line numbers:

```bash
grep -n "error" logfile.txt
```

---

## `find`

Search for files and directories.

Search by name:

```bash
find /home -name "file.txt"
```

Find `.log` files:

```bash
find /var/log -name "*.log"
```

Find directories:

```bash
find /home -type d
```

Find files:

```bash
find /home -type f
```

---

## `wc`

Count lines, words, and characters:

```bash
wc file.txt
```

Count only lines:

```bash
wc -l file.txt
```

---

## `sort`

Sort lines alphabetically:

```bash
sort file.txt
```

---

## `uniq`

Remove adjacent duplicate lines:

```bash
uniq file.txt
```

It is commonly combined with `sort`:

```bash
sort file.txt | uniq
```

---

## `cut`

Extract specific fields or columns.

Example:

```bash
cut -d: -f1 /etc/passwd
```

Here:

```text
-d: → Use : as delimiter
-f1 → Display first field
```

---

# 5. Process Management Commands

These commands are used to view, monitor, control, and manage processes.

---

## `ps`

Display running processes:

```bash
ps
```

Detailed information:

```bash
ps -f
```

Display processes for all users:

```bash
ps aux
```

Another commonly used format:

```bash
ps -ef
```

---

## `top`

`top` provides real-time process monitoring.

```bash
top
```

It displays information such as:

```text
PID
USER
CPU
MEMORY
PROCESS
```

---

## `htop`

`htop` is an interactive process monitoring tool.

```bash
htop
```

If it is not installed:

```bash
sudo apt install htop
```

---

## `kill`

`kill` sends a signal to a process.

```bash
kill PID
```

Example:

```bash
kill 1234
```

The default signal is generally `SIGTERM`, which requests the process to terminate gracefully.

---

## `kill -9`

Forcefully terminate a process:

```bash
kill -9 1234
```

`SIGKILL` cannot be caught or ignored by the target process.

> **Best Practice:** Try `kill PID` first. Use `kill -9` only when necessary.

---

## `pgrep`

Find process IDs based on process names or other matching criteria:

```bash
pgrep nginx
```

---

## `pkill`

Send signals to processes based on their name or matching criteria:

```bash
pkill nginx
```

---

## `jobs`

Display jobs running from the current shell:

```bash
jobs
```

---

## Background Process

Run a command in the background:

```bash
command &
```

Example:

```bash
sleep 100 &
```

---

## `fg`

Bring a background job to the foreground:

```bash
fg
```

---

## `bg`

Continue a stopped job in the background:

```bash
bg
```

---

# 6. Network Commands

Linux provides several commands to inspect network interfaces, IP addresses, routes, connections, DNS, and network connectivity.

---

## `ip`

`ip` is the modern command for network configuration and inspection.

### Show IP Addresses

```bash
ip addr
```

Short form:

```bash
ip a
```

### Show Network Interfaces

```bash
ip link
```

### Show Routing Table

```bash
ip route
```

---

## `ping`

Test basic network connectivity:

```bash
ping google.com
```

Send a specific number of packets:

```bash
ping -c 4 google.com
```

---

## `ss`

Display network sockets and connections.

```bash
ss
```

Show listening TCP and UDP ports:

```bash
ss -tuln
```

Options:

```text
-t → TCP
-u → UDP
-l → Listening
-n → Numeric output
```

---

## `curl`

`curl` is commonly used to communicate with HTTP/HTTPS services.

Request a webpage:

```bash
curl https://example.com
```

Show only HTTP headers:

```bash
curl -I https://example.com
```

It is also useful for testing APIs and web services.

---

## `wget`

`wget` is commonly used to download files.

```bash
wget https://example.com/file.zip
```

---

## `hostname`

Display the system hostname:

```bash
hostname
```

For detailed hostname and system information:

```bash
hostnamectl
```

---

## `dig`

`dig` is used for DNS queries.

```bash
dig google.com
```

On Ubuntu, it may be provided by the `dnsutils` package:

```bash
sudo apt install dnsutils
```

---

## `nslookup`

Another command used to query DNS:

```bash
nslookup google.com
```

---

## `traceroute`

Shows the network path between your system and a destination.

```bash
traceroute google.com
```

If it is not installed:

```bash
sudo apt install traceroute
```

---

# Command Quick Reference

| Category   | Command             | Purpose                                 |
| ---------- | ------------------- | --------------------------------------- |
| Package    | `sudo apt update`   | Update package index                    |
| Package    | `sudo apt upgrade`  | Upgrade installed packages              |
| Package    | `sudo apt install`  | Install package                         |
| Package    | `sudo apt remove`   | Remove package                          |
| Package    | `sudo apt purge`    | Remove package and configuration        |
| Package    | `snap list`         | List installed snaps                    |
| Package    | `sudo snap refresh` | Update snaps                            |
| Package    | `dpkg -l`           | List installed `.deb` packages          |
| Permission | `ls -ltra`          | Detailed listing including hidden files |
| Permission | `chmod`             | Change permissions                      |
| Permission | `chown`             | Change ownership                        |
| Permission | `chgrp`             | Change group ownership                  |
| Text       | `cat`               | Display file contents                   |
| Text       | `less`              | Read files page by page                 |
| Text       | `head`              | Display beginning of file               |
| Text       | `tail`              | Display end of file                     |
| Search     | `grep`              | Search text                             |
| Search     | `find`              | Search files and directories            |
| Text       | `wc`                | Count lines, words, characters          |
| Text       | `sort`              | Sort text                               |
| Text       | `uniq`              | Remove adjacent duplicates              |
| Text       | `cut`               | Extract fields                          |
| Process    | `ps`                | View processes                          |
| Process    | `top`               | Monitor processes                       |
| Process    | `htop`              | Interactive process monitoring          |
| Process    | `kill`              | Send signal to process                  |
| Process    | `pgrep`             | Find process IDs                        |
| Process    | `pkill`             | Signal processes by name                |
| Process    | `jobs`              | View shell jobs                         |
| Process    | `fg`                | Bring job to foreground                 |
| Process    | `bg`                | Continue job in background              |
| Network    | `ip a`              | Show IP/interface information           |
| Network    | `ip route`          | Show routing table                      |
| Network    | `ping`              | Test connectivity                       |
| Network    | `ss`                | View sockets and connections            |
| Network    | `curl`              | Communicate with HTTP/HTTPS services    |
| Network    | `wget`              | Download files                          |
| Network    | `hostnamectl`       | Hostname/system information             |
| Network    | `dig`               | DNS lookup                              |
| Network    | `nslookup`          | DNS lookup                              |
| Network    | `traceroute`        | Trace network path                      |
