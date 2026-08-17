






# Linux Architecture

Linux follows a **layered architecture** where applications interact with hardware through the **Linux Kernel**.

## Architecture Overview

```text
┌──────────────────────────────────────┐
│                USER                  │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│            APPLICATIONS              │
│     Nginx │ Java │ Python │ Git     │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│          SHELL & UTILITIES           │
│     Bash │ ls │ grep │ systemctl    │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│           SYSTEM LIBRARIES           │
│                glibc                 │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│             LINUX KERNEL             │
│                                      │
│ Process │ Memory │ File System       │
│ Network │ Drivers │ Security         │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│              HARDWARE                │
│        CPU │ RAM │ Disk │ NIC        │
└──────────────────────────────────────┘
```

---

## 1. Hardware

The physical resources managed by Linux.

* CPU
* RAM
* Disk / SSD
* Network Interface
* I/O Devices

---

## 2. Linux Kernel

The **Linux Kernel is the core of the Linux operating system**.

It manages hardware resources and provides services to applications.

### Key Responsibilities

* **Process Management** — manages processes and CPU scheduling
* **Memory Management** — manages RAM and virtual memory
* **File System Management** — manages files and storage
* **Networking** — handles network communication
* **Device Drivers** — communicates with hardware devices
* **Security** — manages access, permissions and system capabilities

```text
Application
     │
     ▼
Linux Kernel
     │
     ▼
Hardware
```

---

## 3. System Libraries

System libraries provide APIs that applications use to access operating-system functionality.

**Example:** `glibc`

Simplified flow:

```text
Application
     │
     ▼
System Library
     │
     ▼
System Call
     │
     ▼
Linux Kernel
```

---

## 4. Shell

A **Shell** provides a command-line interface between the user and the operating system.

### Common Shells

* Bash
* Zsh
* Sh
* Fish

Example:

```bash
ls
```

The shell interprets the command and requests the required operation from the operating system.

---

## 5. System Utilities

Linux provides command-line utilities for system administration and daily operations.

```text
ls        → List files
cp        → Copy files
mv        → Move/rename files
rm        → Remove files
grep      → Search text
find      → Find files
ps        → View processes
top       → Monitor processes
systemctl → Manage services
```

---

## 6. Applications

Applications run in **User Space** and use Linux services and resources.

### DevOps Examples

```text
Nginx
Git
Docker
Java
Python
Terraform
kubectl
Jenkins
```

---

# User Space vs Kernel Space

Linux separates normal applications from the kernel.

```text
┌─────────────────────────────────┐
│           USER SPACE            │
│                                 │
│ Applications                    │
│ Shell                           │
│ Git / Docker / Nginx / Java     │
└────────────────┬────────────────┘
                 │
            System Calls
                 │
┌────────────────▼────────────────┐
│          KERNEL SPACE           │
│                                 │
│ Process Management              │
│ Memory Management               │
│ File Systems                    │
│ Networking                      │
│ Device Drivers                  │
│ Security                        │
└────────────────┬────────────────┘
                 │
                 ▼
              Hardware
```

### User Space

Where normal applications and user-level programs run.

### Kernel Space

Where the Linux Kernel runs and manages system resources and hardware.

---

# Command Execution Flow

When a user runs:

```bash
ls
```

The simplified flow is:

```text
User
  ↓
Shell (Bash/Zsh)
  ↓
ls Utility
  ↓
System Library / System Call
  ↓
Linux Kernel
  ↓
File System / Disk
  ↓
Result
  ↓
Terminal
```

---

# Linux Architecture — Key Takeaway

```text
User
  ↓
Applications
  ↓
Shell / Utilities
  ↓
System Libraries
  ↓
Linux Kernel
  ↓
Hardware
```

> **The Linux Kernel is the core layer that connects software with hardware and manages processes, memory, filesystems, networking, devices and security.**

### DevOps Connection

DevOps tools such as **Docker, Kubernetes, Nginx, Git and Terraform** run in the user space and depend on Linux kernel capabilities and underlying system resources.
