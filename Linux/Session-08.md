# Introduction to Microsoft Azure

 ## Overview

 **Microsoft Azure** is a cloud computing platform provided by Microsoft. It allows organizations and individuals to build, deploy, manage, and scale applications and infrastructure using Microsoft's global cloud infrastructure.

 Azure provides a wide range of cloud services, including:

 - Compute
- Storage
- Networking
- Databases
- Identity and Access Management
- Security
- Monitoring
- Analytics
- Artificial Intelligence
- DevOps
- Containers
- Serverless computing

 Instead of purchasing and maintaining physical infrastructure, organizations can provision Azure resources on demand.

---

 # 1\. What is Microsoft Azure?

 Microsoft Azure is a **public cloud platform** that provides infrastructure and managed services over the internet.

 In a traditional on-premises environment, an organization may need to purchase:

```
Physical Server
      |
      +-- CPU
      +-- RAM
      +-- Disk
      +-- Network Card
      |
    Network
      |
   Firewall
      |
 Data Center
```

 With Azure, these capabilities can be consumed as cloud services:

```
                    Microsoft Azure
                          |
        +-----------------+-----------------+
        |                 |                 |
      Compute           Storage          Networking
        |                 |                 |
       VM             Disk/Blob          VNet
```

 The organization does not need to physically purchase the underlying hardware.

---

 # 2\. Why Use Azure?

 Azure provides organizations with the ability to:

 - Provision infrastructure quickly
- Scale resources according to demand
- Deploy applications globally
- Use managed cloud services
- Improve availability and resiliency
- Automate infrastructure
- Implement cloud security
- Reduce infrastructure management overhead
- Pay for resources based on usage

 For example, instead of purchasing a physical server, we can create an **Azure Virtual Machine** within minutes.

---

 # 3\. Microsoft Entra ID

 **Microsoft Entra ID** is Microsoft's cloud-based identity and access management service.

 It was previously known as **Azure Active Directory (Azure AD)**.

 Entra ID is responsible for managing identities and controlling access to applications and Azure resources.

 ### Basic Example

```
                         Microsoft Entra ID
                                |
              +-----------------+-----------------+
              |                 |                 |
            Users             Groups         Applications
              |
        +-----+-----+
        |           |
     Admin       Developer
```

 Entra ID manages identities such as:

 - Users
- Groups
- Applications
- Service principals
- Managed identities

 It also supports authentication and authorization capabilities.

---

 # 4\. Authentication vs Authorization

 Understanding these two concepts is important when working with Entra ID.

 ## Authentication

 **Authentication** answers:

 > "Who are you?"

 Example:

```
User
 |
Username + Password
 |
MFA
 |
Entra ID
 |
Authenticated
```

---

 ## Authorization

 **Authorization** answers:

 > "What are you allowed to do?"

 For example:

```
User
 |
Entra ID
 |
Azure RBAC
 |
+-- Read VM
+-- Start VM
+-- Stop VM
+-- Delete VM
```

 A user may be authenticated successfully but may not have permission to perform a particular operation.

---

 # 5\. Entra ID and Azure

 Entra ID provides the identity layer for Azure.

 A simplified architecture is:

```
                    Microsoft Entra ID
                           |
                    Authentication
                           |
                    Authorization
                           |
                    Azure Resources
                           |
          +----------------+----------------+
          |                |                |
         VM               VNet           Storage
```

 When a user signs into the Azure Portal, their identity is authenticated through Microsoft Entra ID.

 Azure then determines what that user is allowed to access based on permissions and role assignments.

---

 # 6\. Azure Hierarchy

 Azure resources are organized into a hierarchical structure.

 The main hierarchy is:

```
Microsoft Entra Tenant
          |
          v
   Management Groups
          |
          v
     Subscriptions
          |
          v
   Resource Groups
          |
          v
       Resources
```

 A simplified view:

```
Tenant
  |
  +-- Management Group
         |
         +-- Subscription
                |
                +-- Resource Group
                       |
                       +-- Resource
                       +-- Resource
                       +-- Resource
```

 Each level serves a different purpose.

---

 # 7\. Tenant ID

 A **Tenant** represents an organization or identity boundary in Microsoft Entra ID.

 Each Entra tenant has a unique identifier called the **Tenant ID**.

 The Tenant ID is a globally unique identifier, commonly represented as a GUID.

 Example:

```
Tenant ID
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

 The tenant contains identities such as:

 - Users
- Groups
- Applications
- Service principals
- Managed identities

 ### Example

```
                 Entra ID Tenant
                       |
        +--------------+--------------+
        |              |              |
      Users          Groups      Applications
```

 The tenant is primarily an **identity boundary**, while Azure subscriptions are used to organize and manage Azure resources.

---

 # 8\. Management Group

 A **Management Group** is a level above Azure subscriptions.

 Management Groups allow organizations to organize multiple subscriptions into a hierarchy.

```
                 Management Group
                         |
          +--------------+--------------+
          |              |              |
     Subscription A Subscription B Subscription C
```

 Management Groups are useful for applying governance policies and access controls across multiple subscriptions.

 ### Example

 A large organization might structure its environment as:

```
Root Management Group
        |
        +-- Production
        |      |
        |      +-- Prod Subscription 1
        |      +-- Prod Subscription 2
        |
        +-- Non-Production
               |
               +-- Dev Subscription
               +-- Test Subscription
```

---

 # 9\. Subscription

 An **Azure Subscription** is a logical and billing boundary for Azure resources.

 Resources are created inside subscriptions.

 A subscription is commonly used for:

 - Billing
- Access control
- Resource management
- Quotas
- Governance

 ### Example

```
Management Group
       |
       +-- Production Subscription
       |       |
       |       +-- Resource Groups
       |
       +-- Development Subscription
               |
               +-- Resource Groups
```

 Organizations often use separate subscriptions for environments, departments, applications, or business units.

---

 # 10\. Resource Group

 A **Resource Group (RG)** is a logical container for Azure resources.

 Resources that belong to the same application or workload are commonly placed in the same resource group.

 For example:

```
Subscription
     |
     +-- Resource Group: MyApplication
             |
             +-- Virtual Machine
             +-- Virtual Network
             +-- Network Interface
             +-- Public IP
             +-- Disk
```

 A resource group provides a convenient boundary for:

 - Resource organization
- Access control
- Policy
- Monitoring
- Resource lifecycle management

---

 # 11\. Resource

 A **resource** is an individual Azure service or component that you create and manage.

 Examples include:

 - Virtual Machine
- Virtual Network
- Network Interface
- Public IP
- Storage Account
- Managed Disk
- Load Balancer
- SQL Database
- Key Vault

 For example:

```
Resource Group
      |
      +-- VM
      +-- NIC
      +-- Public IP
      +-- Disk
      +-- VNet
```

 Each resource has its own configuration and properties.

---

 # 12\. Complete Azure Hierarchy

 The complete conceptual hierarchy can be represented as:

```
                         Microsoft Entra Tenant
                                  |
                                  v
                         Management Groups
                                  |
                    +-------------+-------------+
                    |                           |
              Management Group             Management Group
                    |                           |
                    v                           v
              Subscription A              Subscription B
                    |                           |
             +------+-------+             +-----+------+
             |              |             |            |
        Resource Group  Resource Group  Resource   Resource Group
             |              |             |
             v              v             v
          Resources       Resources     Resources
```

 ### Hierarchy Summary

 | Level | Purpose |
| --- | --- |
| Tenant | Identity and organizational boundary |
| Management Group | Organizes multiple subscriptions |
| Subscription | Billing, resource, quota, and governance boundary |
| Resource Group | Logical container for resources |
| Resource | Individual Azure service/component |

---

 # 13\. Azure Services

 Azure provides hundreds of services. They can be grouped into major categories.

---

 ## 13.1 Compute

 Compute services provide processing capacity for applications and workloads.

 Examples:

 - Azure Virtual Machines
- Azure Virtual Machine Scale Sets
- Azure App Service
- Azure Functions
- Azure Kubernetes Service (AKS)
- Azure Container Instances

 ### Example

```
Users
  |
  v
Application
  |
  v
Azure Compute
  |
  +-- VM
  +-- App Service
  +-- Functions
  +-- Containers
```

---

 ## 13.2 Networking

 Azure networking services provide connectivity between applications, users, and resources.

 Examples:

 - Azure Virtual Network (VNet)
- Subnets
- Network Security Groups (NSG)
- Azure Load Balancer
- Azure Application Gateway
- Azure VPN Gateway
- Azure DNS
- Azure Firewall
- Azure ExpressRoute

---

 ## 13.3 Storage

 Azure provides different types of storage depending on workload requirements.

 Examples:

 - Azure Blob Storage
- Azure Files
- Azure Queue Storage
- Azure Table Storage
- Managed Disks

 Common use cases include:

 - Files
- Images
- Videos
- Backups
- Logs
- Application data

---

 ## 13.4 Databases

 Azure provides managed database services.

 Examples:

 - Azure SQL Database
- Azure Database for PostgreSQL
- Azure Cosmos DB
- Azure Database for MySQL

 Managed database services reduce the amount of infrastructure administration required from customers.

---

 ## 13.5 Identity and Security

 Azure provides services for identity, access control, security, and secrets management.

 Examples:

 - Microsoft Entra ID
- Azure Role-Based Access Control (RBAC)
- Microsoft Defender for Cloud
- Azure Key Vault
- Microsoft Sentinel

---

 ## 13.6 Monitoring

 Azure provides monitoring and observability services.

 Examples:

 - Azure Monitor
- Log Analytics
- Application Insights
- Alerts

 These services help organizations monitor:

 - Performance
- Availability
- Errors
- Logs
- Metrics
- Application health

---

 ## 13.7 DevOps

 Azure provides services for software development and deployment.

 Examples:

 - Azure DevOps
- Azure Repos
- Azure Pipelines
- Azure Boards
- Azure Artifacts

 These services can be used to implement CI/CD pipelines.

---

 ## 13.8 Containers

 Azure supports containerized workloads.

 Examples:

 - Azure Kubernetes Service (AKS)
- Azure Container Apps
- Azure Container Instances
- Azure Container Registry

---

 ## 13.9 AI and Machine Learning

 Azure provides services for artificial intelligence and machine learning.

 Examples:

 - Azure Machine Learning
- Azure AI services
- Azure OpenAI Service

 These services can be used to build intelligent applications.

---

 # 14\. Example: Creating a Virtual Machine in Azure Portal

 Now let's understand what happens when we create an **Azure Virtual Machine (VM)** using the Azure Portal.

 A VM is not an isolated resource.

 When creating a VM, Azure may create or associate several supporting resources.

 A simplified architecture looks like:

```
                         Azure VM
                            |
             +--------------+--------------+
             |              |              |
            Disk            NIC          Public IP
                            |
                           VNet
                            |
                          Subnet
```

---

 # 15\. VM Creation Through Azure Portal

 When creating a VM through the Azure Portal, we typically configure:

 - Subscription
- Resource Group
- Virtual Machine Name
- Region
- Availability Options
- Image
- VM Size
- Administrator Account
- Authentication
- OS Disk
- Networking
- Monitoring
- Management options

 The exact resources created can vary depending on the options selected.

---

 # 16\. Resources Created for an Azure VM

 A typical VM deployment can involve the following resources:

```
Resource Group
      |
      +-- Virtual Machine
      |
      +-- Managed OS Disk
      |
      +-- Network Interface (NIC)
      |
      +-- Public IP Address
      |
      +-- Virtual Network (VNet)
      |
      +-- Subnet
      |
      +-- Network Security Group (NSG)
```

 Not every deployment necessarily creates every resource as a new resource. For example, an existing VNet, subnet, NSG, or public IP can be selected instead.

---

 # 17\. Virtual Machine

 The **Virtual Machine** is the primary compute resource.

 It provides:

 - CPU
- RAM
- Operating system
- Virtualized compute environment

 Example:

```
VM
 |
 +-- 2 vCPUs
 +-- 8 GB RAM
 +-- Ubuntu / Windows
 +-- OS Disk
 +-- Network Interface
```

 The VM runs the operating system and applications.

---

 # 18\. Managed Disk

 A VM requires storage for its operating system.

 Azure generally uses **Managed Disks** for VM storage.

```
Virtual Machine
      |
      +-- OS Disk
      |
      +-- Data Disk
```

 ### OS Disk

 Contains the operating system.

 Example:

```
Ubuntu
Windows Server
```

 ### Data Disk

 Additional disks can be attached to store application or business data.

```
VM
 |
 +-- OS Disk
 |
 +-- Data Disk 1
 |
 +-- Data Disk 2
```

---

 # 19\. Network Interface Card (NIC)

 The **Network Interface (NIC)** connects the VM to an Azure Virtual Network.

```
VM
 |
NIC
 |
VNet
 |
Subnet
```

 The NIC is responsible for network connectivity for the VM.

 A VM generally needs a network interface to communicate with other resources.

---

 # 20\. Virtual Network (VNet)

 An **Azure Virtual Network (VNet)** provides private networking for Azure resources.

 Example:

```
VNet
 |
 +-- Subnet
       |
       +-- VM
       +-- NIC
```

 A VNet allows Azure resources to communicate with each other and with external networks according to the configured networking rules.

---

 # 21\. Subnet

 A **Subnet** is a smaller network segment inside a VNet.

```
VNet: 10.0.0.0/16
       |
       +-- Subnet: 10.0.1.0/24
              |
              +-- VM1
              +-- VM2
```

 Subnets are commonly used to organize resources and apply networking controls.

---

 # 22\. Public IP Address

 A **Public IP Address** provides internet-facing connectivity when required.

```
Internet
    |
Public IP
    |
   NIC
    |
    VM
```

 A public IP is not mandatory for every VM.

 For example, a VM that only needs private connectivity can operate without a public IP.

---

 # 23\. Network Security Group (NSG)

 A **Network Security Group** contains network security rules that control allowed and denied network traffic.

 Example:

```
NSG
 |
 +-- Allow SSH 22
 +-- Allow HTTP 80
 +-- Allow HTTPS 443
 +-- Deny other traffic
```

 An NSG can be associated with a subnet or network interface, depending on the desired architecture.

---

 # 24\. Complete VM Architecture

 A typical VM created through the Azure Portal can look like this:

```
                              Internet
                                  |
                                  |
                           +-------------+
                           |  Public IP  |
                           +-------------+
                                  |
                                  |
                           +-------------+
                           |     NIC     |
                           +-------------+
                                  |
                                  |
                           +-------------+
                           |     NSG     |
                           +-------------+
                                  |
                                  |
                         +-----------------+
                         |      Subnet     |
                         +-----------------+
                                  |
                                  |
                         +-----------------+
                         |       VNet      |
                         +-----------------+
                                  |
                                  |
                         +-----------------+
                         |       VM        |
                         |-----------------|
                         | CPU / RAM       |
                         | OS              |
                         +-----------------+
                                  |
                                  |
                         +-----------------+
                         |    OS Disk      |
                         +-----------------+
```

---

 # 25\. VM Resources — Summary

 | Resource | Purpose |
| --- | --- |
| Virtual Machine | Provides compute |
| Managed Disk | Stores operating system and data |
| NIC | Provides network connectivity |
| VNet | Provides private network |
| Subnet | Segments the VNet |
| Public IP | Provides public connectivity when required |
| NSG | Controls network traffic |

### Important

 Creating a VM does **not** mean only one Azure resource is created.

 A VM depends on several supporting resources.

 Conceptually:

```
                    VM Deployment
                         |
        +----------------+----------------+
        |                |                |
      Compute          Storage         Network
        |                |                |
        VM           Managed Disk        NIC
                                         |
                              +----------+----------+
                              |                     |
                             VNet                 Public IP
                              |
                           Subnet
                              |
                             NSG
```

 The exact resources created depend on the options selected during VM deployment.

---

 # 26\. End-to-End Azure Hierarchy with VM

 Putting everything together:

```
Microsoft Entra Tenant
        |
        v
Management Group
        |
        v
Subscription
        |
        v
Resource Group
        |
        +-------------------+
        |                   |
        v                   v
   Virtual Machine       Networking
        |                   |
        |             +-----+------+
        |             |            |
        v            VNet         NSG
    OS Disk           |
                       v
                    Subnet
                       |
                       v
                      NIC
                       |
                       v
                   Public IP
```

 This demonstrates how an individual VM fits into the overall Azure resource hierarchy.

---

 # 27\. Key Takeaways

 - **Azure** is Microsoft's cloud computing platform.
- **Microsoft Entra ID** provides identity and access management.
- **Tenant ID** identifies an Entra tenant.
- **Management Groups** organize multiple Azure subscriptions.
- **Subscriptions** provide billing, governance, and resource-management boundaries.
- **Resource Groups** logically organize Azure resources.
- **Resources** are individual Azure services or components.
- Azure provides services for compute, networking, storage, databases, security, monitoring, DevOps, containers, and AI.
- An Azure **VM is not just a single resource**.
- A VM commonly works with supporting resources such as:
  - Managed Disk
  - NIC
  - VNet
  - Subnet
  - NSG
  - Public IP, when required
- The exact resources created during VM deployment depend on the configuration selected in the Azure Portal.

---

 # 28\. Quick Reference

```
                         AZURE
                           |
             +-------------+-------------+
             |                           |
        Entra ID                    Azure Resources
             |                           |
          Tenant                  Management Groups
                                         |
                                   Subscriptions
                                         |
                                   Resource Groups
                                         |
                                      Resources
                                         |
                    +--------------------+--------------------+
                    |                    |                    |
                  Compute             Storage              Network
                    |                    |                    |
                    VM                Disk                 VNet
                                         |                  |
                                        Data              Subnet
                                                            |
                                                           NIC
                                                            |
                                                         NSG / IP
```

 Azure provides the infrastructure and services, while **Entra ID, subscriptions, resource groups, and Azure RBAC** help organizations control **who can access what and how resources are organized and governed**.
