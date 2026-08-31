# Linux Users & Groups Management

* Add and remove users
* Add and remove users from groups
* Create and delete groups
* Lock and unlock user accounts
* Understand primary and supplementary groups
* Check user and group information
* Understand `/etc/passwd`, `/etc/shadow`, and `/etc/group`

---

## Table of Contents

* [1. Understanding Users and Groups](#1-understanding-users-and-groups)
* [2. Check Current User](#2-check-current-user)
* [3. Add a User](#3-add-a-user)
* [4. Set User Password](#4-set-user-password)
* [5. Verify User](#5-verify-user)
* [6. Remove a User](#6-remove-a-user)
* [7. Create a Group](#7-create-a-group)
* [8. Add User to a Group](#8-add-user-to-a-group)
* [9. Why `-aG` is Important](#9-why-ag-is-important)
* [10. Remove User from a Group](#10-remove-user-from-a-group)
* [11. Delete a Group](#11-delete-a-group)
* [12. Lock a User Account](#12-lock-a-user-account)
* [13. Unlock a User Account](#13-unlock-a-user-account)
* [14. Locking a Group](#14-locking-a-group)
* [15. Important Linux Files](#15-important-linux-files)
* [16. Primary vs Secondary Groups](#16-primary-vs-secondary-groups)
* [17. Change Primary Group](#17-change-primary-group)
* [18. Command Cheat Sheet](#18-command-cheat-sheet)

---

# 1. Understanding Users and Groups

Think of a Linux system like a company.

```text
User   = Employee
Group  = Team / Department
Permissions = Access
```

For example:

```text
User: rahul

Groups:
├── rahul
├── developers
└── docker
```

Rahul is a user who belongs to multiple groups.

Linux uses users and groups to control access to files, directories, and other system resources.

A simple way to understand the relationship:

```text
USER
  ↓
belongs to
  ↓
GROUP
  ↓
gets access through
  ↓
FILE / DIRECTORY PERMISSIONS
```

---

# 2. Check Current User

To find out which user you are currently logged in as:

```bash
whoami
```

Example:

```text
rahul
```

To display detailed information about the current user:

```bash
id
```

Example:

```text
uid=1000(rahul) gid=1000(rahul) groups=1000(rahul),1001(developers)
```

### Important Terms

| Term     | Meaning                    |
| -------- | -------------------------- |
| UID      | User ID                    |
| GID      | Group ID                   |
| `groups` | Groups the user belongs to |

---

# 3. Add a User

The `adduser` command is used to create a user on many Linux distributions, particularly Debian/Ubuntu-based systems.

```bash
sudo adduser username
```

Example:

```bash
sudo adduser rahul
```

The command will interactively ask for:

* Password
* Full name
* Other optional user information

Example:

```text
Adding user `rahul' ...
Adding new group `rahul' ...
Adding new user `rahul' with group `rahul' ...
Creating home directory `/home/rahul' ...
```

The user's home directory will normally be:

```text
/home/rahul
```

> **Note:** `adduser` is a higher-level, interactive utility. Its availability and behavior can vary between Linux distributions.

---

# 4. Set User Password

When using `adduser`, a password is normally requested during user creation.

You can also set or change the password later using:

```bash
sudo passwd rahul
```

You will be asked to enter the password twice.

Example:

```text
New password:
Retype new password:
passwd: password updated successfully
```

---

# 5. Verify User

To check information about a user:

```bash
id rahul
```

You can also use:

```bash
getent passwd rahul
```

To check the groups of a user:

```bash
groups rahul
```

---

# 6. Remove a User

To remove a user account:

```bash
sudo deluser rahul
```

To remove the user along with the home directory:

```bash
sudo deluser --remove-home rahul
```

> **Note:** `deluser` is commonly available on Debian/Ubuntu-based systems. On other distributions, user removal is typically performed with `userdel`.

> **Warning:** Removing a user's home directory can permanently delete their files. Always verify the username before performing this operation.

---

# 7. Create a Group

Use `groupadd` to create a group:

```bash
sudo groupadd developers
```

Verify the group:

```bash
getent group developers
```

Example:

```text
developers:x:1001:
```

Here:

```text
developers → Group name
1001       → GID
```

---

# 8. Add User to a Group

To add Rahul to the `developers` group:

```bash
sudo usermod -aG developers rahul
```

### Command Breakdown

```text
usermod      → Modify an existing user
-a           → Append
-G           → Supplementary group
developers   → Group name
rahul        → Username
```

Verify:

```bash
id rahul
```

or:

```bash
groups rahul
```

---

# 9. Why `-aG` is Important

This is one of the most important things to understand.

Suppose Rahul currently belongs to:

```text
rahul
developers
docker
```

If you run:

```bash
sudo usermod -G testers rahul
```

you are specifying the supplementary group list, which can replace the user's existing supplementary group memberships.

You could unintentionally end up with:

```text
rahul
testers
```

instead of:

```text
rahul
developers
docker
testers
```

Therefore, when **adding** an additional supplementary group, use:

```bash
sudo usermod -aG testers rahul
```

### Remember

```text
-aG = Add user to an additional supplementary group
```

---

# 10. Remove User from a Group

Suppose Rahul belongs to:

```text
developers
docker
testers
```

and you want to remove Rahul from `testers`.

Use:

```bash
sudo gpasswd -d rahul testers
```

Example output:

```text
Removing user rahul from group testers
```

Verify:

```bash
groups rahul
```

---

# 11. Delete a Group

To delete a group:

```bash
sudo groupdel developers
```

Verify:

```bash
getent group developers
```

If the group no longer exists, the command will return no matching entry.

> **Important:** Deleting a group does not delete the users who were members of that group.

For example:

```text
developers
├── rahul
├── priya
└── amit
```

Running:

```bash
sudo groupdel developers
```

deletes only the `developers` group.

The users remain.

---

# 12. Lock a User Account

Linux provides commands to lock a user's password.

To lock Rahul:

```bash
sudo passwd -l rahul
```

You can also use:

```bash
sudo usermod -L rahul
```

Check the password status:

```bash
sudo passwd -S rahul
```

A locked password is generally indicated by `L` in the status output.

---

# 13. Unlock a User Account

To unlock Rahul:

```bash
sudo passwd -u rahul
```

Alternatively:

```bash
sudo usermod -U rahul
```

Check the status:

```bash
sudo passwd -S rahul
```

> **Important:** Password locking does not necessarily disable every possible method of accessing an account. For example, SSH keys and other authentication mechanisms may be configured separately.

---

# 14. Locking a Group

Linux does not have a universal command equivalent to:

```bash
passwd -l username
```

for simply "locking" a group.

When someone says:

> "Lock this group"

the actual requirement should be clarified.

It could mean:

* Prevent users from accessing group-owned resources
* Remove users from the group
* Restrict file/directory access
* Manage a group password
* Change group permissions

For example, file access can be controlled through permissions:

```bash
chmod 770 /shared/project
```

Group administration can also be performed using:

```bash
gpasswd
```

The correct method depends on what access needs to be restricted.

---

# 15. Important Linux Files

There are three important files you should know when learning Linux user and group management.

---

## `/etc/passwd`

Contains basic information about user accounts.

View it:

```bash
cat /etc/passwd
```

Example:

```text
rahul:x:1000:1000:Rahul:/home/rahul:/bin/bash
```

The fields are:

```text
Username
Password placeholder
UID
GID
Comment / GECOS
Home directory
Login shell
```

---

## `/etc/shadow`

Contains password hashes and password-aging information.

View it using:

```bash
sudo cat /etc/shadow
```

Example concept:

```text
rahul:$6$....:...
```

> **Security:** Do not manually edit `/etc/shadow`. Use commands such as `passwd` for password management.

---

## `/etc/group`

Contains group information.

View it:

```bash
cat /etc/group
```

Example:

```text
developers:x:1001:rahul,amit
```

The fields represent:

```text
Group name
Password placeholder
GID
Group members
```

---

# 16. Primary vs Secondary Groups

This is an important Linux concept.

A user normally has:

```text
1 Primary Group
+
0 or more Supplementary Groups
```

For example:

```text
User: rahul

Primary Group:
└── rahul

Supplementary Groups:
├── developers
└── docker
```

Check using:

```bash
id rahul
```

Example:

```text
uid=1000(rahul)
gid=1000(rahul)
groups=1000(rahul),1001(developers),999(docker)
```

Here:

```text
gid=1000(rahul)
```

represents the primary group.

The other groups are supplementary groups.

---

# 17. Change Primary Group

To change Rahul's primary group to `developers`:

```bash
sudo usermod -g developers rahul
```

### Important Difference

Change primary group:

```bash
sudo usermod -g developers rahul
```

Add supplementary group:

```bash
sudo usermod -aG developers rahul
```

### Easy Way to Remember

```text
-g   → Primary Group
-G   → Supplementary Groups

-aG  → Add Supplementary Group
```

---

# 18. Command Cheat Sheet

| Task                   | Command                               |
| ---------------------- | ------------------------------------- |
| Check current user     | `whoami`                              |
| Show user information  | `id username`                         |
| Show user's groups     | `groups username`                     |
| Add user               | `sudo adduser username`               |
| Set/change password    | `sudo passwd username`                |
| Delete user            | `sudo deluser username`               |
| Delete user + home     | `sudo deluser --remove-home username` |
| Create group           | `sudo groupadd groupname`             |
| Delete group           | `sudo groupdel groupname`             |
| Add user to group      | `sudo usermod -aG groupname username` |
| Remove user from group | `sudo gpasswd -d username groupname`  |
| Change primary group   | `sudo usermod -g groupname username`  |
| Lock user              | `sudo passwd -l username`             |
| Unlock user            | `sudo passwd -u username`             |
| Check password status  | `sudo passwd -S username`             |
| Query user             | `getent passwd username`              |
| Query group            | `getent group groupname`              |
| View users             | `cat /etc/passwd`                     |
| View groups            | `cat /etc/group`                      |
