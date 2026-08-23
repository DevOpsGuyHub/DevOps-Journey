# Root vs Non-Root User

## Root User
The **superuser / admin** of a Linux system — has full, unrestricted control.

- Username: `root` | User ID (UID): `0` — UID `0` is *always* root, regardless of the name
- Can do anything: create/edit/delete any file (including system files), install or remove software, change any user's password, modify system settings, start/stop any service

```
Root = Full Control
```

## Non-Root User
A **regular user** — the kind of account you normally log in with (e.g. `rahul`, `priya`).

- UID: `1000+` (typically)
- Can manage their own files (e.g. `/home/rahul/`) and run their own programs
- **Cannot** make system-wide changes unless explicitly given permission

**Example — permission denied:**
```bash
rahul@server:~$ rm /etc/important-config.txt
Permission denied
```
This fails because `rahul` is a non-root user and doesn't have rights to touch files under `/etc/`.

---

## Comparison

| Feature | Root User | Non-Root User |
|---|---|---|
| Permission level | Full (unlimited) | Limited |
| UID | 0 | 1000+ |
| Edit system files | ✅ Yes | ❌ No (by default) |
| Install software | ✅ Yes | ❌ No (without sudo) |
| Risk if a command goes wrong | High — can break the whole system | Low — only own files affected |

---

## Letting a Non-Root User Act as Root

Rather than logging in as root directly, a non-root user can borrow root privileges temporarily using `sudo`:

```bash
sudo apt update
```
This says *"give me root permission just for this one command."* It will prompt for your password and check that you're authorized to use `sudo`.

To switch fully into a root shell:
```bash
sudo su -
# or
su root
```

---

## Why Running as Root All the Time Is Risky

```bash
rm -rf /
```
Run as root, a mistake like this can wipe out the entire system — with no confirmation prompt to stop you. As a non-root user, the same mistake would only affect files you own.

---

## Best Practice
> Do daily work as a **non-root user**, and reach for `sudo` only when you actually need admin access.

- Production servers commonly **disable direct root login** entirely
- Working through `sudo` also creates an **audit trail** — logs show *which user* ran a command, instead of everything just showing up as "root"

## One-Line Summary

| Term | Meaning |
|---|---|
| **Root** | Full-access superuser (UID 0) |
| **Non-Root** | Limited-access regular user |
| **sudo** | Temporarily borrow root privileges for a single command |
