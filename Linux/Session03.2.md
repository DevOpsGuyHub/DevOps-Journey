





# 2 .Ports & Security Groups — Simple Notes

## 1. What is a Port?

Think of a server as a building. The building has many rooms, each with a number. That **room number is the Port**.

Every service (website, database, SSH) has its own port, so requests reach the right place.

```
Server (192.168.1.10)
  Port 22   → SSH (login)
  Port 80   → Website
  Port 443  → Secure Website
  Port 3306 → Database
```

**Ports to remember:** 22 (SSH), 80 (HTTP), 443 (HTTPS), 3306 (MySQL)

---

## 2. What is a Security Group?

Outside the building, there's a **guard**. The guard decides who can enter and who can leave.

That guard = **Security Group**. It works outside the server, at the **cloud level** (AWS/Azure, etc.).

```
Internet → [Guard: Security Group] → Server
```

**Example:**
- Let everyone view the website (Port 80) ✅
- Let only your own IP log in via SSH (Port 22) ✅

---

## 3. Inbound vs Outbound

Simple way to remember — look at the **direction of the arrow**:

```
Inbound  →  Traffic coming IN  (someone opens the website)
Outbound →  Traffic going OUT  (server downloads something)
```

| | What it is | Example |
|---|---|---|
| **Inbound** | Traffic heading toward the server | A user opens the website |
| **Outbound** | Traffic leaving the server | Server downloads an update from the internet |

**Default rule (in the cloud):**
```
Inbound  → Blocked by default (must be explicitly allowed)
Outbound → Allowed by default (server can reach out freely)
```
Reason: incoming traffic is riskier, so it's kept restricted by default.

**Stateful (important concept):** If an Inbound request is allowed, its reply (Outbound) is **automatically allowed** — no separate rule needed.

```
User sends request (Inbound ✅) → Server sends reply (Outbound ✅ automatic)
```

---

## How It All Works Together

```
Request arrives
   ↓
Security Group checks → is this allowed?
   ↓ Yes
Server's own Firewall checks → is this port open?
   ↓ Yes
Application (listening on that port) → handles the request
```

> **Common mistake:** Opening a port in the Security Group but forgetting to open it in the server's own firewall too → "Connection Timeout" error. **Both** need to be open.

---

## One-Line Summary

| Term | Simple Meaning |
|---|---|
| **Port** | A service's address/room number |
| **Security Group** | The guard standing outside (cloud firewall) |
| **Inbound** | Traffic coming in |
| **Outbound** | Traffic going out |
