# Linux File Permissions

Linux permissions control **who can read, write, or execute** a file or directory.

---

## Table of Contents

* [1. Understanding Linux Permissions](#1-understanding-linux-permissions)
* [2. Check File Permissions](#2-check-file-permissions)
* [3. Permission Types](#3-permission-types)
* [4. Understanding `ls -l`](#4-understanding-ls--l)
* [5. File Permissions](#5-file-permissions)
* [6. Permission Numbers](#6-permission-numbers)
* [7. Common Permission Values](#7-common-permission-values)
* [8. `chmod` - Change Permissions](#8-chmod---change-permissions)
* [9. Symbolic Method](#9-symbolic-method)
* [10. `chown` - Change Ownership](#10-chown---change-ownership)
* [11. `chgrp` - Change Group](#11-chgrp---change-group)
* [12. Directory Permissions](#12-directory-permissions)
* [13. Recursive Permissions](#13-recursive-permissions)
* [14. File Type Characters](#14-file-type-characters)
* [15. Command Cheat Sheet](#15-command-cheat-sheet)

---

# 1. Understanding Linux Permissions

Linux permissions determine what different users can do with files and directories.

There are three categories of users:

```text
USER      → File owner
GROUP     → Users belonging to the file's group
OTHERS    → All other users
```

There are three basic permissions:

```text
r → read
w → write
x → execute
```

A simple way to understand Linux permissions:

```text
USER
  ↓
GROUP
  ↓
OWNER / GROUP OWNERSHIP
  ↓
PERMISSIONS
  ↓
r / w / x
  ↓
chmod / chown / chgrp
```

---

# 2. Check File Permissions

The `ls` command can be used to view file and directory permissions.

### Basic command

```bash
ls -l
```

### Detailed listing

```bash
ls -ltra
```

`ls -ltra` is commonly useful when you want a detailed listing including hidden files and sorted by modification time.

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

---

# 3. Permission Types

Linux has three basic permission types:

| Permission | Meaning |
| ---------- | ------- |
| `r`        | Read    |
| `w`        | Write   |
| `x`        | Execute |

---

# 4. Understanding `ls -l`

Consider the following output:

```text
-rwxr-xr-- 1 rahul developers 1200 Aug 31 script.sh
```

The permission section is:

```text
-rwxr-xr--
```

Break it down:

```text
- | rwx | r-x | r--
  |     |     |
  |     |     └── Others
  |     └──────── Group
  └────────────── Owner
```

Therefore:

```text
rwx | r-x | r--
 ↓     ↓     ↓
User  Group Others
```

The first character represents the file type.

```text
- → Regular file
d → Directory
l → Symbolic link
```

The remaining nine characters represent permissions:

```text
rwxr-xr--
```

---

# 5. File Permissions

For regular files:

| Permission | Meaning          |
| ---------- | ---------------- |
| `r`        | Read the file    |
| `w`        | Modify the file  |
| `x`        | Execute the file |

For example:

```text
rw-
```

means:

```text
read    ✓
write   ✓
execute ✗
```

---

# 6. Permission Numbers

Linux permissions can also be represented using numbers.

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
rwx = 4 + 2 + 1 = 7

rw- = 4 + 2 + 0 = 6

r-x = 4 + 0 + 1 = 5

r-- = 4 + 0 + 0 = 4

-w- = 0 + 2 + 0 = 2

--x = 0 + 0 + 1 = 1
```

### Permission Table

| Permission | Number |
| ---------- | -----: |
| `---`      |      0 |
| `--x`      |      1 |
| `-w-`      |      2 |
| `-wx`      |      3 |
| `r--`      |      4 |
| `r-x`      |      5 |
| `rw-`      |      6 |
| `rwx`      |      7 |

---

# 7. Common Permission Values

Permissions are commonly written as three numbers:

```text
755
644
700
600
777
```

The three positions represent:

```text
USER | GROUP | OTHERS
```

## `755`

```text
7 | 5 | 5
```

```text
rwx | r-x | r-x
```

Therefore:

```text
755 = rwxr-xr-x
```

Meaning:

```text
Owner  → read + write + execute
Group  → read + execute
Others → read + execute
```

---

## `644`

```text
6 | 4 | 4
```

```text
rw- | r-- | r--
```

Therefore:

```text
644 = rw-r--r--
```

Meaning:

```text
Owner  → read + write
Group  → read
Others → read
```

---

## `700`

```text
7 | 0 | 0
```

```text
rwx | --- | ---
```

Meaning:

```text
Owner  → read + write + execute
Group  → no access
Others → no access
```
---

## `600`

```text
6 | 0 | 0
```

```text
rw- | --- | ---
```

Meaning:

```text
Owner  → read + write
Group  → no access
Others → no access
```

---

## `777`

```text
7 | 7 | 7
```

```text
rwx | rwx | rwx
```

Everyone has:

```text
read + write + execute
```

> **Security Note:** Avoid using `777` unless there is a specific requirement. Giving write access to everyone can create security risks.

---

# 8. `chmod` - Change Permissions

The `chmod` command is used to change file and directory permissions.

### Syntax

```bash
chmod permissions filename
```

### Numeric Method

```bash
chmod 755 script.sh
```

Check the permissions:

```bash
ls -l script.sh
```

---

# 9. Symbolic Method

Permissions can also be changed using symbolic notation.

### User / Group / Others

```text
u → User / Owner
g → Group
o → Others
a → All
```

### Add Execute Permission to Owner

```bash
chmod u+x script.sh
```

### Add Write Permission to Group

```bash
chmod g+w file.txt
```

### Remove Write Permission from Others

```bash
chmod o-w file.txt
```

### Give Execute Permission to Everyone

```bash
chmod a+x script.sh
```

---

# 10. `chown` - Change Ownership

The `chown` command is used to change the owner of a file or directory.

Check ownership:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 rahul developers 1000 file.txt
```

Here:

```text
Owner → rahul
Group → developers
```

Change the owner:

```bash
sudo chown priya file.txt
```

---

## Change Owner and Group

To change both owner and group:

```bash
sudo chown priya:developers file.txt
```

Now:

```text
Owner → priya
Group → developers
```

---

# 11. `chgrp` - Change Group

The `chgrp` command changes the group ownership of a file or directory.

```bash
sudo chgrp developers file.txt
```

The owner remains unchanged.

---

# 12. Directory Permissions

Directory permissions work slightly differently from file permissions.

For directories:

```text
r → List directory contents
w → Create, delete, and rename entries
x → Access / traverse the directory
```

Example:

```text
drwxr-xr-x
```

The first character:

```text
d
```

means it is a directory.

The remaining permissions are:

```text
rwx | r-x | r-x
 ↓     ↓     ↓
User  Group Others
```

---

# 13. Recursive Permissions

To change permissions for a directory and everything inside it, use `-R`.

```bash
chmod -R 755 mydir
```

`-R` means:

```text
Recursive
```

Similarly, ownership can be changed recursively:

```bash
sudo chown -R rahul:developers mydir
```

> **Warning:** Be careful with recursive `chmod` and `chown` commands, especially when working with system directories.

---

# 14. File Type Characters

The first character in `ls -l` output indicates the file type.

```text
- → Regular file
d → Directory
l → Symbolic link
```

Examples:

```text
-rw-r--r-- → Regular file
drwxr-xr-x → Directory
lrwxrwxrwx → Symbolic link
```

---

# 15. Command Cheat Sheet

| Command                   | Purpose                                                              |
| ------------------------- | -------------------------------------------------------------------- |
| `ls -l`                   | View permissions and ownership                                       |
| `ls -ltra`                | Detailed listing including hidden files, sorted by modification time |
| `chmod 755 file`          | Change permissions using numeric mode                                |
| `chmod u+x file`          | Add execute permission for owner                                     |
| `chmod g+w file`          | Add write permission for group                                       |
| `chmod o-r file`          | Remove read permission from others                                   |
| `chmod a+x file`          | Add execute permission for everyone                                  |
| `chown user file`         | Change file owner                                                    |
| `chown user:group file`   | Change owner and group                                               |
| `chgrp group file`        | Change group ownership                                               |
| `chmod -R 755 dir`        | Recursively change permissions                                       |
| `chown -R user:group dir` | Recursively change ownership                                         |

---

## Permission Quick Reference

```text
r = 4
w = 2
x = 1
```

```text
0 = ---
1 = --x
2 = -w-
3 = -wx
4 = r--
5 = r-x
6 = rw-
7 = rwx
```

Common permissions:

```text
644 = rw-r--r--
755 = rwxr-xr-x
700 = rwx------
600 = rw-------
777 = rwxrwxrwx
```

User categories:

```text
u = User / Owner
g = Group
o = Others
a = All
```
