# 1. SSH Authentication in Linux

Authentication answers one question: **"Are you really who you claim to be?"**

Linux supports two common authentication methods for SSH:

1. [Password Authentication](#1-password-authentication)
2. [SSH Key Authentication](#2-ssh-key-authentication)

---

## 1. Password Authentication

The traditional and most familiar method — prove identity using a **username + password**.

### Example Setup
```
Server IP : 192.168.1.10
Username  : rahul
Password  : MyPassword123
```

### Connecting
```bash
ssh rahul@192.168.1.10
```
The server prompts:
```
rahul@192.168.1.10's password:
```

### How It Works
```
Your Laptop
     │  username + password
     ▼
Linux Server ── "Is this password correct?"
     ▼
Authentication successful → Access granted
```

### Where Linux Stores This
| File | Purpose |
|---|---|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Hashed password data |

Linux never stores your password in plain text — it stores a **hash**:
```
MyPassword123  → (hashing) →  $6$abc123$........
```
On login, Linux hashes your input and compares it to the stored hash.

### Pros & Cons
| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Simple and beginner-friendly | Vulnerable to guessing, brute-force, reuse |
| No key setup required | Considered less secure for production |

> Production servers commonly **disable password login** in favor of SSH keys.

---

## 2. SSH Key Authentication

Instead of *"I know the password,"* you prove *"I possess the correct private key."*

### The Key Pair
| Key | Role | Location |
|---|---|---|
| 🔓 **Public Key** | Acts as a "lock" — safe to share, placed on the server | `authorized_keys` on server |
| 🔑 **Private Key** | Acts as the "key" — must stay secret | `~/.ssh/` on your laptop |

> **Rule #1:** Never share your private key.

### Step 1 — Generate a Key Pair
```bash
ssh-keygen
```
Creates:
```
~/.ssh/id_ed25519       → Private key (keep secret)
~/.ssh/id_ed25519.pub   → Public key (share with servers)
```

### Step 2 — Key Placement
```
Your Laptop                          Linux Server
└── ~/.ssh/                          └── /home/rahul/.ssh/
    └── id_ed25519  🔑 (SECRET)          └── authorized_keys  🔓 (STORED)
```

### Step 3 — Authentication Flow
```
Your Laptop                         Linux Server
    │── "Login as rahul" ─────────────▶│
    │◀──── authentication challenge ───│
    │── proves possession of ─────────▶│
    │   private key                    │
    │◀──────── Authentication OK ──────│
    │              Logged in            │
```
The server verifies key possession **without ever receiving the private key itself** — this is the core security benefit.

---

## Password vs SSH Key — Comparison

| Aspect | Password | SSH Key |
|---|---|---|
| Mechanism | Shared secret (password) | Cryptographic key pair |
| Ease of use | Simple | Slightly more technical |
| Login step | Password entered each time | Usually passwordless |
| Security | Vulnerable to brute-force | Strong cryptographic security |
| Common usage | Basic systems | Servers, cloud, DevOps, CI/CD |
| What to protect | The password | The private key |

---

## Real-World Use Case — Managing Multiple Servers

Managing passwords across many servers doesn't scale well:
```
Server 1  → password
Server 2  → password
...
Server 100 → password
```

With SSH keys, one private key can authenticate across all servers:
```
Admin Laptop
    │ Private Key
    ▼
  SSH Key
    ├── Server 1
    ├── Server 2
    ├── Server 3
    └── Server 100
```
Each server simply stores the admin's **public key** in `~/.ssh/authorized_keys`.

This is why SSH keys are the standard in **Linux administration, DevOps, cloud (AWS/Azure), Git, and CI/CD pipelines**.

---

## ⚠️ Public vs Private Key — Don't Confuse These

| Key File | Type | Safe to Share? |
|---|---|---|
| `id_ed25519.pub` | Public Key | ✅ Yes |
| `id_ed25519` | Private Key | ❌ Never |

If your private key is compromised, anyone holding it can authenticate as you on every system where it's trusted.

---

## Essential Commands for Beginners

| Task | Command |
|---|---|
| Connect to a server | `ssh username@server-ip` |
| Generate a key pair | `ssh-keygen` |
| Copy public key to server | `ssh-copy-id username@server-ip` |
| List your SSH keys | `ls -la ~/.ssh/` |
| View your public key | `cat ~/.ssh/id_ed25519.pub` |
| Check authorized keys on server | `cat ~/.ssh/authorized_keys` |

---

## Quick Recap

| Method | Core Idea |
|---|---|
| **Password Authentication** | "I know the password." |
| **SSH Key Authentication** | "I possess the private key matching the public key the server trusts." |

**Learning path for freshers:**
```
ssh → ssh-keygen → public key → private key → authorized_keys


ssh <UserName>@<Public-IP> ---------- Username + Password
```





