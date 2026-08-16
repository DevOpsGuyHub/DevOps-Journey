# Software, SDLC and Introduction to DevOps

## 1. What is Software?

**Software** is a set of programs and instructions that tells a computer or system what to do.

### Example: Zomato

Zomato is a software-based platform that provides:

* Restaurant discovery
* Food ordering
* Online payment
* Order tracking
* Delivery tracking
* Notifications

---

## 2. SDLC — Software Development Life Cycle

**SDLC** is a structured process used to build, test, deploy, and maintain software.

### Traditional SDLC

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

### Zomato Example

Suppose Zomato wants to introduce **Scheduled Food Delivery**.

| Phase        | Example                                    |
| ------------ | ------------------------------------------ |
| Idea         | Allow users to schedule an order           |
| Requirements | Define business and technical requirements |
| Design       | Design UI and system architecture          |
| Development  | Developers implement the feature           |
| Testing      | QA validates the feature                   |
| Deployment   | Release the feature to production          |
| Maintenance  | Fix bugs and improve the feature           |

---

# 3. Traditional Software Deployment

In the traditional model, teams usually worked in separate silos.

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

Development, Operations, Infrastructure, and Testing had separate responsibilities.

### Example

For a new Zomato feature:

1. Developers complete the code.
2. QA performs testing.
3. Release team prepares the deployment.
4. Operations manually deploys it.
5. Infrastructure team manages servers.
6. Production is monitored after deployment.

---

# 4. Problems with Traditional Deployment

### 1. Team Silos

Development and Operations worked independently.

**Result:** Communication gaps and conflicts.

### 2. Slow Releases

Deployments involved multiple manual steps and approvals.

**Result:** Releases could take days or weeks.

### 3. Manual Deployment

Manual deployments can introduce:

* Human errors
* Configuration mistakes
* Inconsistent deployments

### 4. Environment Differences

Development, testing, and production environments could have different configurations.

**Common problem:**

> "It works in Development but fails in Production."

### 5. Late Feedback

Production problems were often discovered only after deployment.

```text
Development → Testing → Production → Problem discovered
```

### 6. Infrastructure Was Slow to Provision

Creating and configuring servers manually required significant time and effort.

### 7. High Deployment Risk

More manual steps and larger releases increased the possibility of production failures.

---

# 5. Entry of DevOps

DevOps emerged as organizations needed to:

* Release software faster
* Reduce deployment failures
* Improve collaboration
* Automate repetitive work
* Get faster feedback from production
* Improve reliability

The central idea was to bring **Development and Operations closer together**.

---

# 6. What is DevOps?

> **DevOps is a culture and set of practices that brings Development and Operations together and uses automation and continuous feedback to deliver software faster, reliably, and repeatedly.**

DevOps is **not just a collection of tools**.

```text
DevOps
├── Culture
├── Collaboration
├── Automation
├── CI/CD
├── Infrastructure as Code
├── Security
└── Monitoring & Feedback
```

---

# 7. DevOps Lifecycle

Modern DevOps follows a continuous lifecycle:

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

The important concept is the **continuous feedback loop**.

---

# 8. Zomato Example — DevOps in Practice

Suppose Zomato introduces **One-Click Reorder**.

### Plan

Product and engineering teams define the requirement.

### Code

Developers implement the feature and push code to Git.

### Build

CI pipeline automatically builds the application.

### Test

Automated tests validate the changes.

### Security & Quality

Tools can perform:

* Code quality checks
* SAST
* Dependency scanning
* Container scanning

### Release

A validated build is packaged and made ready for deployment.

### Deploy

CD automation deploys the application to the target environment.

### Operate

The application serves real users in production.

### Monitor

Teams monitor:

* Application errors
* API latency
* CPU and memory
* Database performance
* Traffic
* Availability

### Feedback

Suppose monitoring shows:

```text
Order API latency
200 ms → 3 seconds
```

The team investigates the problem, fixes it, tests the change, and deploys a new version.

This creates a **continuous improvement cycle**.

---

# 9. How DevOps Solved Traditional Problems

| Traditional Problem          | DevOps Approach                   |
| ---------------------------- | --------------------------------- |
| Development/Operations silos | Collaboration                     |
| Manual deployments           | Deployment automation             |
| Slow releases                | CI/CD                             |
| Environment differences      | Infrastructure as Code            |
| Manual infrastructure        | Terraform / IaC                   |
| Late testing                 | Automated testing                 |
| Late production feedback     | Continuous monitoring             |
| High deployment risk         | Smaller, automated releases       |
| Difficult rollback           | Versioning and automated rollback |

---

# 10. Automation in DevOps

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
Security Scan
   ↓
Artifact / Container Image
   ↓
CD Pipeline
   ↓
Deployment
   ↓
Monitoring
```

The goal is to make software delivery **repeatable and automated**.

---

# 11. Infrastructure as Code

Traditional infrastructure:

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

Infrastructure can be:

* Version controlled
* Reviewed
* Automated
* Reused
* Recreated consistently

---

# 12. Monitoring and Feedback

DevOps does not stop at deployment.

The goal is:

> **Build → Deploy → Observe → Learn → Improve**

Example:

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
```

Monitoring provides real-world feedback about application health and user experience.

---

# 13. Traditional vs DevOps

| Traditional           | DevOps                                |
| --------------------- | ------------------------------------- |
| Team silos            | Collaboration                         |
| Manual processes      | Automation                            |
| Large releases        | Smaller, frequent releases            |
| Slow feedback         | Continuous feedback                   |
| Manual infrastructure | Infrastructure as Code                |
| Manual deployment     | CI/CD                                 |
| Reactive monitoring   | Continuous observability              |
| High deployment risk  | Controlled and repeatable deployments |

---

# 14. The Complete Picture

### Traditional Model

```text
Idea
 ↓
Development
 ↓
Testing
 ↓
Deployment
 ↓
Infrastructure
 ↓
Monitoring
```

Typical problems:

**Silos + Manual Work + Slow Releases + Late Feedback + High Risk**

### DevOps Model

```text
Plan
 ↓
Code
 ↓
Build
 ↓
Test
 ↓
Security
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

Core principles:

**Collaboration + Automation + CI/CD + IaC + Security + Monitoring + Continuous Feedback**

---

## Key Takeaway

> **DevOps evolved to solve the gap between software development and operations by combining collaboration, automation, continuous delivery, infrastructure automation, and continuous feedback.**
