<div align="center">

# Azure Load Balancer
### Deep-Dive Notes · Concepts · Traffic Flow · Components · Real-World Example

![Azure](https://img.shields.io/badge/Microsoft_Azure-Load_Balancer-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![OSI Layer](https://img.shields.io/badge/OSI-Layer%204-6A5ACD?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-16825D?style=for-the-badge)

**A practical guide to Layer 4 load balancing in Microsoft Azure**

</div>

---

## Contents
1. [What is Azure Load Balancer?](#1-what-is-azure-load-balancer)
2. [Why do we need it?](#2-why-do-we-need-it)
3. [Traffic flow](#3-traffic-flow)
4. [Types](#4-types-of-azure-load-balancer)
5. [Core components](#5-core-components)
6. [Distribution algorithm and session persistence](#6-distribution-algorithm-and-session-persistence)
7. [Health probes](#7-health-probes)
8. [Practical example](#8-practical-example-a-web-application)
9. [Key takeaways](#9-key-takeaways)
10. [Official documentation](#official-microsoft-documentation)

---

## 1. What is Azure Load Balancer?

**Azure Load Balancer** is a Layer 4 (Transport layer) service that distributes incoming **TCP and UDP network flows** across backend resources such as Azure Virtual Machines and Virtual Machine Scale Set instances.

In simple terms, it gives clients a single frontend IP address. Behind that address, multiple backend servers can handle traffic. Azure selects an eligible backend for each network flow based on the configured rules and backend health.

### Think of it like a reception desk

A building has one main entrance and several reception desks. Visitors arrive at the main entrance; a coordinator directs each visitor to an eligible desk. Visitors do not need to know each desk's location.

| Real-world concept | Azure Load Balancer concept |
|---|---|
| Main entrance | Frontend IP configuration |
| Coordinator's routing policy | Load-balancing rule |
| Reception desks | Backend pool members |
| Desk availability check | Health probe |
| A visitor's network conversation | TCP/UDP flow |

> **Core concept:** Azure Load Balancer works at Layer 4. It does not inspect HTTP URLs, URL paths, cookies, or application content to decide where to send traffic.

## 2. Why do we need it?

Without a load balancer, clients may connect to a single server. If that server fails or becomes overloaded, the application can become slow or unavailable.

Azure Load Balancer helps with:

- **High availability:** new flows can be sent to healthy backend instances.
- **Scalability:** more backend instances can be added as demand grows.
- **A stable entry point:** clients connect to a frontend IP rather than tracking every VM.
- **Traffic distribution:** eligible network flows can be spread across the backend pool.
- **Private and public access patterns:** use a public frontend for internet-facing traffic or a private frontend for internal traffic.

A load balancer alone does not guarantee application availability. The backend VMs, application, probes, network security, and deployment design must also be configured correctly.

## 3. Traffic flow

### Step-by-step request flow

```text
                    CLIENT
                       |
                       | TCP/UDP request
                       v
          +---------------------------+
          | Frontend IP Configuration |
          |       Public / Private    |
          +---------------------------+
                       |
                       v
          +---------------------------+
          | Load-balancing Rule        |
          | Protocol + Frontend Port   |
          | Backend Pool + Backend Port|
          +---------------------------+
                       |
                       v
          +---------------------------+
          | Backend Pool               |
          |   VM-A   VM-B   VM-C        |
          +---------------------------+
                       |
             Select a healthy backend
                       |
                       v
                 APPLICATION
                       |
                       v
             Response returns to client
```

1. **Client sends traffic.** For example, a browser starts a TCP connection to the frontend IP on port `443`.
2. **Frontend receives the flow.** The frontend IP is the address clients connect to.
3. **A rule matches the traffic.** The rule specifies protocol, frontend port, backend pool, backend port, and associated probe.
4. **Azure selects an eligible backend.** The instance must be considered healthy for the relevant rule.
5. **The backend processes the request.** The selected VM's application handles the traffic.
6. **Response traffic follows the established flow mapping.** Azure maintains the flow mapping so the response reaches the client correctly.

### What if a backend VM fails?

Suppose VM-A, VM-B, and VM-C are in the backend pool. If VM-B fails its health probe, Azure avoids assigning **new flows** to that unhealthy instance. New flows can be sent to VM-A or VM-C.

Do not assume that existing connections are instantly migrated to another VM. An established connection generally cannot be transparently moved to a different server without application-level support.

## 4. Types of Azure Load Balancer

There are two useful ways to classify Azure Load Balancer: by **frontend access** and by **deployment scope**.

### A. By frontend access

| Type | Frontend | Typical use |
|---|---|---|
| **Public Load Balancer** | Public IP address | Internet-facing applications and public endpoints |
| **Internal Load Balancer (ILB)** | Private IP address in a virtual network | Internal APIs, application tiers, and private services |

**Public example:** Users on the internet connect to a public IP; the load balancer distributes eligible traffic to backend web VMs.

**Internal example:** A web tier connects to a private frontend IP for an internal API. Traffic stays on the private network path rather than exposing that frontend as a public IP.

### B. By deployment scope

| Scope | What it does | Typical use |
|---|---|---|
| **Regional Load Balancer** | Balances traffic to backend resources in one Azure region | A standard application deployment within a region |
| **Cross-region Load Balancer** | Provides a global frontend and distributes traffic across regional load balancers | Applications deployed in multiple Azure regions |

A cross-region load balancer is not merely a regional load balancer with more VMs. Each region still needs a correctly configured regional application and load-balancing setup.

### SKU note

For new deployments, use **Standard Load Balancer** and follow current Microsoft guidance. **Basic Load Balancer was retired on September 30, 2025**, so older tutorials that depend on the Basic SKU may no longer apply.

## 5. Core components

### 5.1 Frontend IP configuration

The frontend is the IP address through which clients access the load-balanced service.

- A **public frontend** uses a public IP address.
- An **internal frontend** uses a private IP address from a virtual network subnet.
- A load balancer can have multiple frontend configurations.

**Example:** A website's frontend is `20.50.60.70`. Customers connect to `20.50.60.70:443`; they do not need to know the private IP addresses of the backend VMs.

### 5.2 Backend pool

The backend pool is the group of resources that can receive traffic from the load balancer. It can contain supported backend resources such as VM network interfaces or Virtual Machine Scale Set instances.

| Backend member | Private IP | Role |
|---|---|---|
| VM-A | `10.0.1.4` | Web server |
| VM-B | `10.0.1.5` | Web server |
| VM-C | `10.0.1.6` | Web server |

Azure chooses from eligible pool members according to the configured rule and health state.

### 5.3 Health probe

A health probe checks whether a backend instance should receive traffic. Depending on the scenario, probes can use TCP, HTTP, or HTTPS.

- **TCP probe:** checks whether a configured TCP port is reachable.
- **HTTP probe:** requests a path such as `/health` and checks the response.
- **HTTPS probe:** checks a configured endpoint over HTTPS where supported.

A probe is not a complete end-to-end test of every application feature. If `/health` always returns success while the application is broken, Azure may continue to consider the VM healthy. Design the endpoint to represent meaningful readiness.

### 5.4 Load-balancing rule

A rule maps matching frontend traffic to a backend pool. It specifies the protocol and ports, the backend pool, the health probe, and applicable distribution settings.

**Example:**

| Setting | Example |
|---|---|
| Frontend | Public frontend |
| Protocol | TCP |
| Frontend port | `443` |
| Backend port | `443` |
| Backend pool | `web-backend-pool` |
| Probe | HTTPS `/health` |

This means TCP traffic arriving at the frontend on port `443` can be distributed to healthy backend instances on port `443`.

### 5.5 Inbound NAT rule

An inbound Network Address Translation (NAT) rule maps a specific frontend port to a specific backend resource and port. It is typically a **one-to-one port mapping**, not a rule for distributing a service across the whole backend pool.

**Example:** A frontend port could map to a management port on one VM. Avoid exposing management ports broadly to the internet; apply strict network access controls.

### 5.6 Outbound rule

An outbound rule defines how backend instances use the load balancer's frontend for outbound connections, including outbound SNAT behavior in applicable designs.

Outbound connectivity depends on the overall Azure network architecture. An inbound load-balancing rule does **not** automatically mean outbound internet access is configured correctly.

### 5.7 High Availability (HA) Ports rule

An HA Ports rule supports scenarios such as network virtual appliances where traffic across **all ports** needs to be handled by the configured backend pool, subject to the rule's protocol and configuration.

This is a specialized network scenario, not the usual choice for a web app that only needs TCP ports `80` and `443`.

## 6. Distribution algorithm and session persistence

Azure Load Balancer uses **hash-based distribution**. It does not simply send each request to the next VM in a round-robin sequence.

The commonly described five-tuple includes:

1. Source IP address
2. Source port
3. Destination IP address
4. Destination port
5. IP protocol

Azure hashes network-flow information to map a flow to a backend. Distribution is therefore not guaranteed to be perfectly even at every moment. Different clients and connection patterns can produce different traffic patterns across VMs.

### Session persistence options

Depending on the rule configuration, persistence can use:

- **None:** normal flow distribution based on the default hash.
- **Client IP:** uses client and destination IP information so flows from the same client IP can remain associated with the same backend under the configured behavior.
- **Client IP and protocol:** uses client IP, destination IP, and protocol information.

Session persistence is **not** the same as application session storage. If user sessions must survive backend changes, consider shared session storage or stateless authentication rather than relying only on load-balancer persistence.

## 7. Health probes

A health probe informs Azure whether a backend instance should receive new flows for a rule.

### Example

Assume each web VM exposes a health endpoint:

```text
https://10.0.1.4/health
https://10.0.1.5/health
https://10.0.1.6/health
```

The probe checks the configured endpoint for each backend. If VM-B fails the required check, its health state can become unhealthy and Azure avoids assigning new flows to it for the associated rule.

### Good probe design

- Use a dedicated health endpoint when appropriate.
- Ensure the endpoint reports meaningful application readiness.
- Confirm the probe protocol, port, and path match the service.
- Check NSG rules and the guest OS firewall if probes fail.
- Treat probe intervals and failure thresholds as operational settings; choose them based on the application's recovery behavior.

**Troubleshooting clue:** If every backend appears unhealthy, verify the probe protocol, port/path, application listener, NSG rules, and operating-system firewall before concluding that the load balancer itself is faulty.

## 8. Practical example: a web application

Imagine an online shopping website running on three Azure VMs in one virtual network.

### Architecture

```text
                   INTERNET USERS
                         |
                         | HTTPS :443
                         v
                Public Frontend IP
                   20.50.60.70
                         |
                         v
              Azure Standard Load Balancer
                         |
                    Rule: TCP 443
                         |
                    Backend Pool
                +--------+--------+
                |        |        |
                v        v        v
              VM-A     VM-B     VM-C
            10.0.1.4 10.0.1.5 10.0.1.6
                |        |        |
                +--------+--------+
                    Web app tier
```

### Configuration summary

| Component | Example configuration |
|---|---|
| Load balancer | Standard, regional, public |
| Frontend | `20.50.60.70` |
| Backend pool | `web-backend-pool` |
| Backend VMs | VM-A, VM-B, VM-C |
| Rule | TCP `443` → backend port `443` |
| Probe | HTTPS `/health` |
| Network security | Allow only required traffic from appropriate sources |

### Scenario A — Normal operation

1. A customer connects to `20.50.60.70:443`.
2. The TCP `443` rule matches.
3. Azure selects an eligible healthy backend for the flow.
4. That VM serves the request.
5. The response returns to the customer using the established flow mapping.

### Scenario B — VM-B becomes unhealthy

1. VM-B stops passing the configured health probe.
2. Azure marks VM-B unhealthy for that probe.
3. New flows are directed to healthy instances, VM-A or VM-C.
4. When VM-B recovers and passes the probe again, it can become eligible for new flows.

### Scenario C — Traffic grows

If traffic increases, add more VM instances or use a Virtual Machine Scale Set with suitable autoscaling. Ensure new instances are included in the backend configuration and pass the health probe before receiving traffic.

**Design reminder:** Load balancing distributes network flows. It does not automatically scale the application, repair a failed deployment, or guarantee an exactly equal number of requests per VM.

## 9. Key takeaways

- Azure Load Balancer is a **Layer 4 TCP/UDP** service.
- The frontend is the entry point; the backend pool contains eligible destinations.
- Rules define how matching frontend traffic reaches the backend pool.
- Health probes help prevent new flows from going to unhealthy instances.
- Public and internal frontends support different access patterns.
- Regional and cross-region load balancers solve different deployment-scope needs.
- Hash-based distribution is not round-robin; perfectly equal distribution is not guaranteed.
- Load Balancer differs from Application Gateway: Application Gateway provides Layer 7 HTTP/HTTPS routing features.

## Official Microsoft documentation

- [Azure Load Balancer components](https://learn.microsoft.com/azure/load-balancer/components)
- [Manage Azure Load Balancer](https://learn.microsoft.com/en-us/azure/load-balancer/manage)
- [Azure Load Balancer overview](https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-overview)

---

<div align="center">

**Azure Load Balancer · Concept guide and practical reference**

</div>
