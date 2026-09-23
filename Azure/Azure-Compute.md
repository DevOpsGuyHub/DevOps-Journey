# 1. What is Compute?

In cloud computing, **Compute** means the processing power required to run an application, software, website, API, script, or workload.

For example, a website may contain:

```text
HTML
CSS
JavaScript
Backend Code
Database Connection
```

Something needs to execute this code.

That "something" is **Compute**.

Azure provides multiple ways to obtain compute resources:

```text
Azure Compute
│
├── Virtual Machines
├── Virtual Machine Scale Sets
├── App Service
├── Containers
├── Azure Kubernetes Service (AKS)
│
└── Service Models
    ├── IaaS
    ├── PaaS
    └── SaaS
```

---

# 2. Why Do We Need Compute?

Suppose you write a Python application:

```python
print("Hello Azure")
```

The code itself is just a file.

To execute it, you need resources such as:

```text
CPU
RAM
Operating System
Storage
Network
```

Traditionally, you would purchase a physical server.

```text
Application
     ↓
Operating System
     ↓
Physical Server
     ↓
Data Center
```

With Azure:

```text
Application
     ↓
Azure Compute Service
     ↓
Microsoft Data Center
```

Azure provides the underlying infrastructure.

---

# 3. Traditional Data Center vs Azure Compute

## Traditional Data Center

You purchase and manage:

```text
Physical Server
CPU
RAM
Hard Disk
Network Card
Power
Cooling
Rack
Internet Connection
```

You are responsible for much of the infrastructure.

---

## Azure

You can create an Azure compute resource such as:

```text
Azure VM
```

Azure manages the underlying physical infrastructure.

You focus on the parts of the environment that belong to you based on the service model you selected.

---

# 4. Main Azure Compute Services

| Service                   | Basic Idea                                                      |
| ------------------------- | --------------------------------------------------------------- |
| Virtual Machine           | Rent a virtual server                                           |
| VM Scale Set              | Manage many VMs as a group                                      |
| App Service               | Run web applications without managing the underlying servers    |
| Azure Container Instances | Run individual containers                                       |
| AKS                       | Run and orchestrate containerized applications using Kubernetes |

---

# 5. Virtual Machine (VM)

## 5.1 What is a VM?

A **Virtual Machine** is a software-defined computer running on physical infrastructure.

A physical server can host multiple virtual machines:

```text
Physical Server
┌──────────────────────────────┐
│                              │
│       Hypervisor             │
│                              │
├──────────┬──────────┬────────┤
│ VM-1     │ VM-2     │ VM-3   │
│ Ubuntu   │ Windows  │ Ubuntu │
└──────────┴──────────┴────────┘
```

Each VM behaves like an independent computer.

---

# 6. What Does a VM Contain?

An Azure VM generally involves:

```text
VM
│
├── CPU
├── RAM
├── OS Disk
├── Data Disk
├── NIC
├── Private IP
├── Public IP (optional)
├── NSG
├── Operating System
└── Application
```

---

# 7. VM Architecture

A simplified Azure VM architecture:

```text
                  Internet
                     │
                     ↓
               Public IP
                     │
                     ↓
                   NIC
                     │
                     ↓
                   NSG
                     │
                     ↓
                  Azure VM
              ┌─────────────┐
              │ Application │
              │     ↓       │
              │     OS      │
              │     ↓       │
              │    CPU      │
              │    RAM      │
              └─────────────┘
                 │       │
                 ↓       ↓
              OS Disk  Data Disk
```

---

# 8. VM Components

## 8.1 CPU

CPU executes instructions.

Example:

```text
Application
     ↓
CPU
     ↓
Instruction execution
```

More CPU capacity generally allows an application to process more work.

Azure VM sizes specify the CPU resources available to the VM.

Examples:

```text
2 vCPU
4 vCPU
8 vCPU
16 vCPU
```

---

# 9. What is vCPU?

**vCPU = Virtual CPU**

Azure exposes virtual processing resources to a VM.

Conceptually:

```text
Physical Azure Host
       │
       ├── vCPU → VM1
       ├── vCPU → VM1
       ├── vCPU → VM2
       └── vCPU → VM2
```

The exact relationship between physical processors and vCPUs depends on the underlying Azure infrastructure and VM family.

---

# 10. RAM

RAM is temporary working memory.

Example:

```text
VM
├── 2 vCPU
└── 8 GB RAM
```

Applications use RAM while they are running.

Example:

```text
Java Application
      ↓
RAM
      ↓
CPU
```

Insufficient memory can cause applications to become slow or fail.

---

# 11. VM Size

When creating a VM, you select a VM size.

A VM size determines resources and capabilities such as:

```text
CPU
RAM
Network capability
Disk capability
Other hardware characteristics
```

Conceptual example:

```text
Small VM
2 CPU
4 GB RAM

Medium VM
4 CPU
16 GB RAM

Large VM
8 CPU
32 GB RAM
```

The exact specifications depend on the selected Azure VM family and region.

---

# 12. VM Families

Azure provides different VM families for different workloads.

## General Purpose

Balanced CPU and memory.

Useful for:

```text
Web servers
Application servers
Development environments
Small databases
```

---

## Compute Optimized

Designed for CPU-intensive workloads.

Useful for:

```text
CPU-intensive applications
Batch processing
Application servers
```

---

## Memory Optimized

Provides higher memory capacity.

Useful for:

```text
Large databases
In-memory workloads
Analytics
Caching
```

---

## Storage Optimized

Designed for workloads requiring high storage throughput or I/O performance.

Useful for:

```text
Data-intensive applications
Large-scale databases
Storage-heavy workloads
```

---

## GPU

Designed for GPU-intensive workloads.

Useful for:

```text
Machine Learning
AI
Rendering
Graphics
Deep Learning
```

---

# 13. VM Image

Before creating a VM, you need an **image**.

An image is a template used to create a VM.

Examples:

```text
Ubuntu
Windows Server
Red Hat Enterprise Linux
SUSE Linux
```

Think of an image as:

> **A template from which a VM is created.**

---

# 14. OS Disk

The OS disk contains the operating system.

For example:

```text
Ubuntu VM

OS Disk
│
├── /boot
├── /
├── /etc
├── /var
└── OS files
```

The OS disk is used to boot the virtual machine.

---

# 15. Data Disk

A data disk is used for application and persistent data storage.

Example:

```text
VM
│
├── OS Disk
│     └── Ubuntu
│
└── Data Disk
      └── Application Data
```

You might use a data disk for:

```text
Database files
Application files
Logs
Documents
```

---

# 16. Temporary Disk

Azure VMs can have temporary/local storage depending on the VM type.

This storage is intended for temporary data.

Examples:

```text
Cache
Temporary files
Swap/page files
```

Important:

> **Do not use temporary disk as your primary persistent data storage.**

Its behavior and availability depend on the VM type and underlying infrastructure.

---

# 17. NIC

**NIC = Network Interface Card**

In Azure, a VM communicates with the network through a NIC.

Flow:

```text
Application
     ↓
VM
     ↓
NIC
     ↓
Subnet
     ↓
VNet
```

A NIC can be associated with:

```text
Private IP
Public IP association
NSG
```

---

# 18. Private IP

A private IP is used for communication inside private networks.

Example:

```text
VM1
10.0.1.4

VM2
10.0.1.5
```

They can communicate privately if networking and security rules allow it.

---

# 19. Public IP

A public IP can provide internet-based connectivity to a resource.

Example:

```text
Internet
    ↓
Public IP
    ↓
NIC
    ↓
VM
```

Having a public IP does **not automatically mean every port is accessible**.

Network security rules still control traffic.

---

# 20. NSG

**NSG = Network Security Group**

An NSG controls network traffic using security rules.

Example:

```text
Internet
   ↓
Port 22
   ↓
NSG
   ↓
Allow / Deny
   ↓
VM
```

Example rules:

```text
Allow HTTPS 443
Allow SSH 22 from an approved source
Deny unwanted traffic
```

For Windows administration:

```text
RDP → TCP 3389
```

For Linux:

```text
SSH → TCP 22
```

---

# 21. Availability Set

Availability Sets distribute VMs across different fault and update domains within the Azure infrastructure.

Conceptually:

```text
Availability Set
│
├── Fault Domain 1 → VM1
├── Fault Domain 2 → VM2
│
├── Update Domain 1 → VM1
└── Update Domain 2 → VM2
```

This reduces the possibility that all VMs are affected by the same planned or unplanned infrastructure event.

---

# 22. Availability Zone

Availability Zones are physically separate locations within an Azure region.

Conceptually:

```text
Azure Region
│
├── Zone 1
│    └── VM1
│
├── Zone 2
│    └── VM2
│
└── Zone 3
     └── VM3
```

If one zone experiences an infrastructure problem, workloads in another zone may remain available.

---

# 23. Availability Set vs Availability Zone

| Feature              | Availability Set                       | Availability Zone            |
| -------------------- | -------------------------------------- | ---------------------------- |
| Scope                | Within Azure datacenter infrastructure | Separate physical zones      |
| Main purpose         | Reduce correlated VM failures          | Provide physical isolation   |
| VM distribution      | Fault/update domains                   | Zones                        |
| Typical architecture | Multiple VMs in one region             | VMs distributed across zones |

---

# 24. VM Extension

VM Extensions allow you to perform post-deployment configuration and management tasks.

Examples:

```text
Install software
Run scripts
Configure monitoring
Configure security agents
```

Example:

```text
Create VM
   ↓
VM Extension
   ↓
Install Nginx
   ↓
Configure Nginx
```

---

# 25. VM Scale Sets

## What is VMSS?

**VM Scale Set (VMSS)** allows you to create and manage a group of VMs as a scalable resource.

Instead of manually creating:

```text
VM1
VM2
VM3
VM4
VM5
```

you define a scale set.

```text
VM Scale Set
│
├── VM1
├── VM2
├── VM3
├── VM4
└── VM5
```

---

# 26. Why VMSS?

Suppose your application receives:

```text
100 users
```

You may need:

```text
2 VMs
```

During peak traffic:

```text
10,000 users
```

You may need:

```text
10 VMs
```

VMSS can automatically adjust the number of VM instances according to configured scaling policies.

---

# 27. VMSS Scaling

There are two major scaling concepts.

## Scale Out

Increase the number of VM instances.

```text
2 VMs
 ↓
5 VMs
```

---

## Scale In

Decrease the number of VM instances.

```text
5 VMs
 ↓
2 VMs
```

---

# 28. Vertical vs Horizontal Scaling

## Vertical Scaling

Increase resources of one machine.

```text
4 CPU / 16 GB
       ↓
8 CPU / 32 GB
```

This is:

**Scale Up**

---

## Horizontal Scaling

Increase the number of machines.

```text
VM1
VM2
```

becomes:

```text
VM1
VM2
VM3
VM4
```

This is:

**Scale Out**

---

# 29. VMSS Example

Suppose an e-commerce website uses VMSS.

Normal traffic:

```text
Internet
    ↓
Load Balancer
    ↓
VMSS
├── VM1
└── VM2
```

Peak traffic:

```text
Internet
    ↓
Load Balancer
    ↓
VMSS
├── VM1
├── VM2
├── VM3
├── VM4
├── VM5
└── VM6
```

After traffic decreases:

```text
VM1
VM2
```

The scale set can reduce instances based on its scaling configuration.

---

# 30. Load Balancer with VMSS

A common architecture is:

```text
                 Internet
                    ↓
              Load Balancer
                    ↓
          ┌─────────┼─────────┐
          ↓         ↓         ↓
         VM1       VM2       VM3
```

The load balancer distributes incoming traffic among healthy instances.

---

# 31. When Should You Use VM?

Use a VM when you need significant control over the operating system or server environment.

Examples:

```text
Custom software
Legacy applications
Special OS configuration
Custom agents
Specific system-level requirements
Lift-and-shift workloads
```

---

# 32. Azure App Service

## 32.1 What is App Service?

Azure App Service is a managed platform for hosting web applications, APIs, and related web workloads.

You don't need to manage the underlying VM operating system yourself.

Conceptually:

```text
Your Application
       ↓
Azure App Service
       ↓
Azure-managed infrastructure
```

---

# 33. VM vs App Service

## VM

You manage more of:

```text
OS
Patching
Runtime
Application
Security configuration
Server configuration
```

## App Service

Azure manages much of:

```text
Physical infrastructure
Host OS/platform
Platform maintenance
```

You primarily manage:

```text
Application
Application configuration
Deployment
Identity
Scaling configuration
```

---

# 34. App Service Supports

App Service can host supported web application runtimes such as:

```text
.NET
Java
Node.js
Python
PHP
Containers
```

It can be used for:

```text
Websites
REST APIs
Backend applications
Business applications
```

---

# 35. App Service Architecture

```text
                    Internet
                       │
                       ↓
                Azure App Service
                       │
                ┌──────┴──────┐
                │ Application  │
                │     Code     │
                └──────────────┘
                       │
                 Database/API
```

---

# 36. App Service Plan

This is an important concept.

An **App Service Plan** defines the compute resources and pricing tier on which App Service apps run.

Think of it as:

```text
App Service Plan
│
├── CPU
├── RAM
├── Region
├── Pricing tier
├── Scaling capability
└── Infrastructure capacity
```

Multiple apps can run within the same App Service Plan, subject to the plan's available capacity and configuration.

Example:

```text
App Service Plan
│
├── Website
├── Backend API
└── Admin Portal
```

---

# 37. App Service Scaling

App Service supports different scaling approaches depending on the selected tier and configuration.

## Scale Up

Move to a larger or more capable App Service Plan tier.

```text
Small
 ↓
Medium
 ↓
Large
```

## Scale Out

Increase the number of application instances.

```text
Instance 1
Instance 2
Instance 3
```

---

# 38. Deployment Slots

App Service supports deployment slots in applicable tiers.

Example:

```text
Production
     │
     └── myapp.azurewebsites.net

Staging
     │
     └── staging slot
```

You can deploy a new version to staging, test it, and then swap slots.

Conceptually:

```text
Old Version
Production
    ↓
New Version
Staging
    ↓
Testing
    ↓
Slot Swap
    ↓
Production
```

This can reduce deployment downtime and deployment risk.

---

# 39. App Service Environment Variables

Application configuration can be provided through App Service configuration.

Example:

```text
DATABASE_HOST
DATABASE_NAME
API_URL
ENVIRONMENT
```

For secrets, use appropriate Azure security services such as:

```text
Azure Key Vault
Managed Identity
```

Avoid hardcoding credentials into source code.

---

# 40. App Service Deployment Methods

Common deployment approaches include:

```text
Azure DevOps
GitHub Actions
ZIP deployment
Container deployment
Other supported CI/CD mechanisms
```

Typical DevOps flow:

```text
Developer
   ↓
Git
   ↓
CI Pipeline
   ↓
Build
   ↓
Test
   ↓
Deploy
   ↓
Azure App Service
```

---

# 41. Containers

## What is a Container?

A container packages an application together with the dependencies required to run it.

Example:

```text
Application
+
Libraries
+
Runtime
+
Configuration
        ↓
     Container
```

---

# 42. Why Containers?

Without containers:

```text
Application
   ↓
"Works on my laptop"
   ↓
Fails in another environment
```

Containers help standardize the runtime environment.

```text
Developer Machine
      ↓
Same Container Image
      ↓
Test
      ↓
Production
```

---

# 43. Container vs VM

This section has been intentionally removed as requested.

---

# 44. Container Image

A container image is a packaged artifact used to create containers.

Example:

```text
nginx:latest
```

or:

```text
mycompany/myapp:1.0
```

The image contains the application and required dependencies.

---

# 45. Azure Container Registry

**ACR = Azure Container Registry**

ACR stores container images and related artifacts.

Example:

```text
Developer
    ↓
docker build
    ↓
myapp:1.0
    ↓
ACR
    ↓
AKS / App Service / Container Instance
```

ACR is a private registry service integrated with Azure.

---

# 46. Azure Container Instances

**Azure Container Instances (ACI)** allows you to run containers without managing a VM or Kubernetes cluster directly.

Conceptually:

```text
Container Image
      ↓
Azure Container Instances
      ↓
Running Container
```

Useful for:

```text
Simple container execution
Short-lived workloads
Jobs
Development/testing
Burst workloads
```

---

# 47. Containers vs ACI vs AKS

| Requirement                      | Suitable concept |
| -------------------------------- | ---------------- |
| Package application              | Container        |
| Store container image            | ACR              |
| Run a simple container           | ACI              |
| Run a complex container platform | AKS              |
| Full server control              | VM               |
| Managed web application          | App Service      |

---

# 48. Azure Kubernetes Service (AKS)

## What is Kubernetes?

Kubernetes is a platform for orchestrating containers.

Suppose you have:

```text
Frontend
Backend
Payment Service
Notification Service
Auth Service
```

Each service may run in containers.

Managing hundreds of containers manually becomes difficult.

Kubernetes provides mechanisms to automate container workload management.

---

# 49. What Does Kubernetes Do?

Kubernetes provides capabilities such as:

```text
Container scheduling
Scaling
Service discovery
Rolling deployments
Self-healing
Networking
Configuration
Secrets
Workload management
```

---

# 50. AKS

**AKS = Azure Kubernetes Service**

AKS is Azure's managed Kubernetes service.

Conceptually:

```text
Azure
│
└── AKS Cluster
    │
    ├── Control Plane
    │
    └── Node Pools
         │
         ├── Node
         │    ├── Pod
         │    └── Pod
         │
         └── Node
              ├── Pod
              └── Pod
```

---

# 51. AKS Architecture Details

This section has been intentionally removed as requested.

---

# 52. AKS Worker Nodes

This section has been intentionally removed as requested.

---

# 53. Pod

This section has been intentionally removed as requested.

---

# 54. AKS Example

This section has been intentionally removed as requested.

---

# 55. AKS Self-Healing

This section has been intentionally removed as requested.

---

# 56. AKS Scaling

This section has been intentionally removed as requested.

---

# 57. AKS Networking

This section has been intentionally removed as requested.

---

# 58. AKS Storage

This section has been intentionally removed as requested.

---

# 59. AKS Monitoring

This section has been intentionally removed as requested.

---

# 60. IaaS

**IaaS = Infrastructure as a Service**

Azure provides infrastructure.

Examples:

```text
Azure VM
Disk
Network
VNet
NIC
```

You manage more of the stack.

Conceptually:

```text
Application       → Customer
Runtime           → Customer
Operating System  → Customer
Virtualization    → Azure
Hardware          → Azure
Networking infra  → Azure
```

---

# 61. PaaS

**PaaS = Platform as a Service**

Azure manages more of the underlying platform.

Examples:

```text
Azure App Service
Azure SQL Database
Azure Functions
```

Conceptually:

```text
Application       → Customer
Application Code  → Customer
Runtime/Platform  → Azure
OS                → Azure
Hardware          → Azure
```

---

# 62. SaaS

**SaaS = Software as a Service**

You consume a complete software product.

Examples include cloud-hosted applications such as:

```text
Microsoft 365
Microsoft Teams
Salesforce
ServiceNow
```

You primarily manage:

```text
Users
Configuration
Data
Business settings
```

The provider manages the application platform and infrastructure.

---

# 63. IaaS vs PaaS vs SaaS — Simple Example

Imagine you want to run a website.

## IaaS

You rent a VM.

```text
Azure VM
   ↓
Install/configure OS
   ↓
Install Nginx
   ↓
Install runtime
   ↓
Deploy application
```

You have more control and more operational responsibility.

---

## PaaS

Use App Service.

```text
App Service
    ↓
Deploy Application
```

Azure manages much of the infrastructure and platform.

---

## SaaS

Use an already-built application.

```text
Complete Software
       ↓
Login
       ↓
Use it
```

You don't build or manage the underlying application platform.

---

# 64. Shared Responsibility Model

Cloud security follows a shared responsibility model.

The cloud provider and customer share responsibilities.

Conceptually:

```text
                Responsibility
                     │
        ┌────────────┴────────────┐
        │                         │
    Microsoft                  Customer
        │                         │
Physical infrastructure      Data
Physical security            Identity
Datacenter                    Access
Underlying hardware          Application
                             Configuration
```

The exact responsibility boundary depends on the service.

---

# 65. Responsibility Comparison

| Layer               | VM       | App Service | SaaS     |
| ------------------- | -------- | ----------- | -------- |
| Physical hardware   | Azure    | Azure       | Provider |
| Datacenter          | Azure    | Azure       | Provider |
| Host infrastructure | Azure    | Azure       | Provider |
| Guest OS            | Customer | Azure       | Provider |
| Runtime             | Customer | Managed     | Provider |
| Application         | Customer | Customer    | Provider |
| Data                | Customer | Customer    | Customer |
| User access         | Customer | Customer    | Customer |

---

# 66. Control vs Management

A useful conceptual rule is:

```text
More Infrastructure Control
          ↑
          │
         VM
          │
     App Service
          │
    Managed Containers
          │
         SaaS
          │
          ↓
Less Infrastructure Management
```

AKS is a special case because Azure manages the Kubernetes control plane, while customers still manage significant aspects of workloads, node pools, networking, security, and Kubernetes configuration.

---

# 67. VM vs App Service vs Container vs AKS

| Feature                | VM             | App Service      | Container           | AKS                                    |
| ---------------------- | -------------- | ---------------- | ------------------- | -------------------------------------- |
| OS management          | High           | Low              | Host-managed        | Node/platform largely managed by Azure |
| Container required     | No             | No               | Yes                 | Yes                                    |
| Kubernetes             | No             | No               | No                  | Yes                                    |
| Infrastructure control | High           | Lower            | Depends on service  | High at orchestration/workload level   |
| Scaling                | Manual/VMSS    | Built-in options | Depends on service  | Kubernetes-based                       |
| Best for               | Custom servers | Web/API apps     | Container workloads | Large/complex container platforms      |

---

# 68. How to Choose Azure Compute

Ask these questions.

## Question 1

Do I need complete OS control?

```text
YES → VM
```

---

## Question 2

Do I primarily need to host a web/API application?

```text
YES → App Service may fit
```

---

## Question 3

Is my application containerized?

```text
YES
 ↓
Simple workload → Container service such as ACI
Complex platform → AKS
```

---

## Question 4

Do I have a complex container platform or many containerized services?

```text
YES → AKS may be appropriate
```

---

## Question 5

Do I need an existing complete software product?

```text
YES → SaaS
```

---

# 69. Real-World E-Commerce Example

Suppose we have an e-commerce application.

Components:

```text
Frontend
Backend
Payment
Authentication
Notification
Database
```

A possible architecture could use:

```text
Internet
    ↓
Azure Front Door
    ↓
Application Gateway
    ↓
AKS
    ↓
Containerized Applications
    ↓
Azure Database
```

Supporting services might include:

```text
Azure Container Registry
Azure Key Vault
Azure Monitor
Log Analytics
Azure Storage
Azure Cache
```

---

# 70. VM-Based Architecture

For a traditional application:

```text
Internet
   ↓
Load Balancer
   ↓
VMSS
   ├── VM
   ├── VM
   └── VM
        ↓
    Application
        ↓
     Database
```

---

# 71. App Service Architecture

```text
Internet
    ↓
App Service
    ↓
Application
    ↓
Azure SQL
```

This can be simpler operationally than managing individual VMs.

---

# 72. Production DevOps Flow

A typical modern application deployment process can look like:

```text
Developer
    ↓
GitHub / Azure Repos
    ↓
CI Pipeline
    ↓
Build
    ↓
Unit Test
    ↓
Security Scan
    ↓
Build Container
    ↓
Push Image
    ↓
Azure Container Registry
    ↓
Deployment
    ↓
AKS / App Service
    ↓
Monitoring
    ↓
Alerts
```

---

# 73. Important Interview Questions

## Q1. What is Azure Compute?

Azure Compute provides processing resources for running applications and workloads in Azure.

---

## Q2. VM vs App Service?

### VM

```text
More control
More management
```

### App Service

```text
Less infrastructure management
Managed application platform
```

---

## Q3. What is VMSS?

VMSS is a service for deploying and managing a group of Azure VMs with capabilities for scaling and instance management.

---

## Q4. Scale Up vs Scale Out?

```text
Scale Up  → Increase resources of an existing instance
Scale Out → Increase the number of instances
```

---

## Q5. What is a container?

A container packages an application and its dependencies into an isolated, portable runtime environment.

---

## Q6. What is ACI?

Azure Container Instances provides a way to run containers without directly managing a VM or Kubernetes cluster.

---

## Q7. What is AKS?

AKS is Azure's managed Kubernetes service for running and orchestrating containerized workloads.

---

## Q8. What is ACR?

Azure Container Registry is a managed private registry for storing and distributing container images and related artifacts.

---

## Q9. What is IaaS?

Infrastructure as a Service provides infrastructure resources such as virtual machines, storage, and networking while leaving more configuration responsibility with the customer.

---

## Q10. What is PaaS?

Platform as a Service provides a managed application platform so the customer can focus more on application development and deployment rather than infrastructure management.

---

## Q11. What is SaaS?

Software as a Service provides a complete software application managed by the service provider.

---

# 74. One-Line Memory Trick

Remember these definitions:

```text
VM
↓
"I want a server."

VMSS
↓
"I want many servers that can scale."

App Service
↓
"I want to host my web/API application without managing servers."

Container
↓
"I want my application packaged consistently."

ACI
↓
"I want to run a container simply."

AKS
↓
"I have containerized workloads and need Kubernetes orchestration."

IaaS
↓
"Give me infrastructure."

PaaS
↓
"Give me a platform."

SaaS
↓
"Give me the complete software."
```

---

# 75. Recommended Teaching Sequence

For beginners, teach the concepts in this order:

```text
Day 1
│
├── What is Compute?
├── Physical Server vs VM
├── VM architecture
├── CPU
├── RAM
├── Disk
├── NIC
├── IP
├── NSG
└── VM creation

Day 2
│
├── VM Images
├── OS Disk
├── Data Disk
├── Temporary Disk
├── VM Sizes
├── Availability Set
├── Availability Zone
├── VM Extension
└── VM troubleshooting

Day 3
│
├── VMSS
├── Scale Up
├── Scale Out
├── Load Balancer
└── Autoscaling

Day 4
│
├── App Service
├── App Service Plan
├── Scaling
├── Deployment Slots
├── Configuration
└── CI/CD deployment

Day 5
│
├── Containers
├── Docker
├── Image
├── Container
├── Dockerfile
├── Registry
└── ACR

Day 6
│
├── Kubernetes
├── Cluster
├── AKS
└── Why Kubernetes is used

Day 7
│
├── IaaS
├── PaaS
├── SaaS
├── Shared Responsibility
├── VM vs App Service
├── VM vs Container
├── Container vs AKS
└── Real-world architecture
```

---

# 76. Final Mental Model

The complete picture:

```text
                         AZURE COMPUTE
                              │
        ┌─────────────────────┼──────────────────────┐
        │                     │                      │
       VM                    PaaS                 Containers
        │                     │                      │
      VMSS               App Service               ACI
        │                                            │
        │                                           AKS
        │
        └──────────── Infrastructure
                         │
                       IaaS


                  SERVICE MODELS
                       │
          ┌────────────┼────────────┐
          │            │            │
         IaaS         PaaS         SaaS
          │            │            │
        VM         App Service   Complete App
```
