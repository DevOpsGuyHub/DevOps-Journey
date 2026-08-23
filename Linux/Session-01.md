# Software, SDLC, Traditional Deployment & Introduction to DevOps

## 1. What is Software?

**Software** is a set of programs and instructions that tells a computer or system what to do.

### Example — Zomato

Zomato is a software-based platform that allows users to:

* Discover restaurants
* Order food
* Make payments
* Track orders
* Receive notifications

From a DevOps perspective, software is more than source code:

```text
Software
├── Source Code
├── Dependencies
├── Configuration
├── Database
└── Infrastructure
```

---

# 2. SDLC — Software Development Life Cycle

**SDLC** is a structured process used to **plan, develop, test, deploy, and maintain software**.

```text
Idea
  ↓
Requirements
  ↓
Design
  ↓
Development
  ↓
Testing
  ↓
Deployment
  ↓
Maintenance
```

### Example — Zomato

Suppose Zomato wants to introduce **Scheduled Food Delivery**.

| Phase            | What happens?                              |
| ---------------- | ------------------------------------------ |
| **Idea**         | Introduce scheduled delivery               |
| **Requirements** | Define business and technical requirements |
| **Design**       | Design UI, APIs, database and architecture |
| **Development**  | Developers write the code                  |
| **Testing**      | QA validates functionality                 |
| **Deployment**   | Release the feature to production          |
| **Maintenance**  | Fix bugs and improve the feature           |

### Important

SDLC defines **how software is developed**.

It does not by itself solve the problems of **how software is delivered and operated efficiently**.

---

# 3. Traditional Software Deployment

In the traditional model, Development, Testing, Release, Infrastructure, and Operations were usually handled by separate teams.

```text
Development
     ↓
   Testing
     ↓
 Release Team
     ↓
 Operations
     ↓
 Production
     ↓
 Monitoring
```

A typical deployment looked like:

```text
Developer
    ↓
Write Code
    ↓
Build
    ↓
Test
    ↓
Create Release Package
    ↓
Handover to Operations
    ↓
Manual Configuration
    ↓
Manual Deployment
    ↓
Production
```

Each team completed its part and **handed over the work to the next team**.

---

# 4. Problems with Traditional Deployment

As applications became larger and releases became more frequent, this approach created several challenges.

### 1. Team Silos

Development and Operations had separate responsibilities and priorities.

```text
Development  ──── X ──── Operations
                 ↑
          Communication Gap
```

**Result:** Miscommunication, delays, and conflicts.

---

### 2. Manual Deployment

Servers, configurations, and application releases were often handled manually.

**Result:**

* Human errors
* Configuration mistakes
* Inconsistent deployments

---

### 3. Slow Releases

Multiple handoffs, manual activities, and approvals made releases slow.

```text
Development
     ↓
     QA
     ↓
Release Team
     ↓
Operations
     ↓
Production
```

**Result:** A simple change could take days or weeks to reach production.

---

### 4. Environment Differences

Development, Testing, and Production environments could have different configurations.

```text
Development → Works
Testing     → Works
Production  → Fails
```

Common statement:

> **"It works on my machine."**

---

### 5. Late Feedback

Problems were often discovered only after the application reached production.

```text
Development
     ↓
Testing
     ↓
Production
     ↓
Problem discovered
```

The longer the feedback cycle, the more expensive the problem becomes to fix.

---

### 6. Manual Infrastructure

Servers and infrastructure were provisioned and configured manually.

**Result:**

* Slow provisioning
* Configuration drift
* Difficult replication
* Higher operational effort

---

### 7. High Deployment Risk

Large releases combined with manual processes increased the possibility of production failures.

```text
Large Change
     +
Manual Process
     +
Environment Differences
     ↓
Higher Deployment Risk
```

---

# 5. Why DevOps Emerged

Organizations needed a better way to:

* Release software faster
* Reduce deployment failures
* Remove team silos
* Automate repetitive tasks
* Provision infrastructure consistently
* Get faster feedback
* Improve reliability

This need led to the adoption of **DevOps practices**.

### Traditional Model

```text
Development                 Operations
     │                           │
     │     Handover / Gap        │
     └────────────X──────────────┘
                  ↓
          Deployment Problems
```

### DevOps Model

```text
          Development
               ↕
        Collaboration
               ↕
          Operations
               ↓
          Automation
               ↓
      Continuous Feedback
```

---

# 6. What is DevOps?

> **DevOps is a culture and set of practices that brings Development and Operations together, using collaboration, automation, and continuous feedback to deliver software faster, reliably, and repeatedly.**

DevOps is **not just a collection of tools**.

```text
                    DevOps
                       │
       ┌───────────────┼────────────────┐
       ↓               ↓                ↓
 Collaboration     Automation       Continuous
                                      Feedback
       │               │                │
       ├───────────────┼────────────────┤
       ↓               ↓                ↓
      CI/CD            IaC           Monitoring
                       │
                       ↓
                    Security
```

---

# 7. DevOps Lifecycle

DevOps transforms software delivery into a **continuous lifecycle**.



```text
PLAN
  ↓
CODE
  ↓
BUILD
  ↓
TEST
  ↓
RELEASE
  ↓
DEPLOY
  ↓
OPERATE
  ↓
MONITOR
  ↓
FEEDBACK
  └──────────────→ PLAN
```

The key difference is the **continuous feedback loop**.

---

# 8. Zomato — DevOps in Practice

Suppose Zomato introduces **One-Click Reorder**.

```text
Plan
 ↓
Code
 ↓
Build
 ↓
Test
 ↓
Security & Quality
 ↓
Release
 ↓
Deploy
 ↓
Operate
 ↓
Monitor
 ↓
Feedback
 └────────────→ Plan
```

### Flow

<img width="3000" height="2000" alt="25225452_7041508" src="https://github.com/user-attachments/assets/f421125e-6a0d-42d1-a026-05d6af82be19" />


**Plan**
Define the feature and requirements.

**Code**
Developers implement the feature and push code to Git.

**Build**
CI pipeline builds the application.

**Test**
Automated tests validate the changes.

**Security & Quality**
Code quality, SAST, dependency, and container scans are performed.

**Release**
A validated artifact or container image is created.

**Deploy**
CD automation deploys the application.

**Operate**
The application serves real users.

**Monitor**
Teams monitor errors, latency, CPU, memory, database performance, traffic, and availability.

**Feedback**
Production data is used to identify problems and improve the application.

### Example

Suppose monitoring detects:

```text
Order API Latency
     ↓
200 ms → 3 seconds
     ↓
Alert
     ↓
Investigation
     ↓
Fix
     ↓
Test
     ↓
Deploy
```

The fix goes through the same delivery cycle again.

This creates **continuous improvement**.

---

# 9. How DevOps Solves Traditional Problems

| Traditional Problem     | DevOps Solution                   |
| ----------------------- | --------------------------------- |
| Team silos              | Collaboration                     |
| Manual deployment       | Deployment automation             |
| Slow releases           | CI/CD                             |
| Environment differences | Infrastructure as Code            |
| Manual infrastructure   | Terraform / IaC                   |
| Late testing            | Automated testing                 |
| Late feedback           | Continuous monitoring             |
| High deployment risk    | Smaller, repeatable releases      |
| Difficult rollback      | Versioning and automated rollback |

---

# 10. Automation — Traditional vs DevOps

### Traditional

```text
Code
 ↓
Manual Build
 ↓
Manual Testing
 ↓
Manual Deployment
```

### DevOps

```text
Code Push
    ↓
CI Pipeline
    ↓
Build
    ↓
Test
    ↓
Security & Quality
    ↓
Artifact / Container Image
    ↓
CD Pipeline
    ↓
Deployment
    ↓
Monitoring
    ↓
Feedback
```

### Goal

> **Make software delivery repeatable, consistent, reliable, and automated.**

---

# 11. Infrastructure as Code

Traditional approach:

```text
Request Server
     ↓
Approval
     ↓
Manual Provisioning
     ↓
Manual Configuration
```

DevOps approach:

```text
Infrastructure Code
        ↓
     Terraform
        ↓
Cloud Infrastructure
```

Infrastructure can now be:

* Version controlled
* Reviewed
* Automated
* Reused
* Consistently recreated

---

# 12. Monitoring & Feedback

DevOps does not end with deployment.

```text
Application
     ↓
Metrics / Logs / Traces
     ↓
Monitoring
     ↓
Alert
     ↓
Investigation
     ↓
Fix
     ↓
New Deployment
     ↓
Monitoring
```

Core principle:

> **Build → Deploy → Observe → Learn → Improve**

---

# 13. Traditional vs DevOps

| Traditional           | DevOps                     |
| --------------------- | -------------------------- |
| Team silos            | Collaboration              |
| Manual processes      | Automation                 |
| Large releases        | Smaller, frequent releases |
| Slow feedback         | Continuous feedback        |
| Manual infrastructure | Infrastructure as Code     |
| Manual deployment     | CI/CD                      |
| Reactive monitoring   | Continuous monitoring      |
| High deployment risk  | Repeatable deployments     |

---

# 14. Complete Connection

```text
                         SOFTWARE
                            │
                            ↓
                           SDLC
                            │
                            ↓
                 Traditional Development
                            │
                            ↓
                 Traditional Deployment
                            │
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
      Team Silos       Manual Work       Slow Releases
          │                 │                 │
          └─────────────────┼─────────────────┘
                            ↓
                  Deployment Problems
                            │
                            ↓
                       DEVOPS
                            │
        ┌───────────────────┼───────────────────┐
        ↓                   ↓                   ↓
 Collaboration          Automation        Feedback
        │                   │                   │
        ├───────────────┬───┴───────────────┬───┤
        ↓               ↓                   ↓
      CI/CD             IaC              Security
        │               │                   │
        └───────────────┼───────────────────┘
                        ↓
                  Faster & Reliable
                  Software Delivery
```

---

# Key Takeaway

```text
SOFTWARE
   ↓
SDLC
   ↓
Traditional Development & Deployment
   ↓
Manual Work + Team Silos + Slow Releases
   ↓
Deployment & Operational Problems
   ↓
DEVOPS
   ↓
Collaboration + Automation + CI/CD
+ IaC + Security + Monitoring
   ↓
Continuous Feedback
   ↓
Faster + Reliable + Repeatable Delivery
```

> **SDLC tells us how software is developed. DevOps improves how software is built, delivered, deployed, operated, and continuously improved.**

<img width="700" height="540" alt="image" src="https://github.com/user-attachments/assets/3bd7f6ab-0b2e-4948-994b-24f48438cce3" />
