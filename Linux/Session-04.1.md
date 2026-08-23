# Types of Path in Linux

Linux uses two types of paths to locate files and directories: **Absolute Path** and **Relative Path**.

---

## 1. Absolute Path

Starts from the **root (`/`)** and gives the complete address of a file — works the same regardless of your current location.

```bash
/home/USER/projects/app.py
/etc/nginx/nginx.conf
/var/log/syslog
```

### Characteristics
- Always begins with `/`
- Works from **any directory**
- Longer to type, but never ambiguous

### Example
```bash
cd /home/USER/projects
```
This works no matter where you currently are in the filesystem.

---

## 2. Relative Path

Defined **relative to your current directory**. Does not start with `/`.

```bash
projects/app.py
../logs/error.log
./script.sh
```

### Characteristics
- Depends on the **current working directory**
- Shorter and quicker to type
- Result changes based on where you run it from

### Special Symbols

| Symbol | Meaning |
|---|---|
| `.` | Current directory |
| `..` | One level up (parent directory) |
| `../..` | Two levels up |

### Example
```bash
pwd
# /home/USER

cd projects/app
# Works only because the current directory is /home/USER
```

```bash
cd ..
# Moves up one directory (/home/USER → /home)
```

---

## Absolute vs Relative — Comparison

| Feature | Absolute Path | Relative Path |
|---|---|---|
| Starts from | `/` (root) | Current location |
| Length | Longer | Shorter |
| Works from any directory | ✅ Yes | ❌ No |
| Best for | Scripts, configs, cron jobs | Quick manual navigation |

---

## Example — The Difference in Practice

```
Current directory: /home/USER

Absolute: cd /home/USER/projects/app   → always works
Relative: cd projects/app                → only works from /home/USER
```

Running the relative path from a different location fails:
```bash
cd /var/log
cd projects/app
# Error: No such file or directory
```
because `/var/log/projects/app` doesn't exist.

---

## Best Practice

> Use **Absolute Paths** in scripts, cron jobs, and configuration files so they work reliably regardless of execution context.
> Use **Relative Paths** for quick, everyday terminal navigation.

---

## Summary

| Term | Meaning |
|---|---|
| **Absolute Path** | Full address from `/`, works anywhere |
| **Relative Path** | Short address based on current location |
| `.` | Current directory |
| `..` | Parent directory (one level up) |
