# Azure Load Balancer — Questions

**
Basic Questions**

1. What is Azure Load Balancer?
2. What is the primary purpose of a load balancer?
3. At which OSI layer does Azure Load Balancer operate?
4. Which network protocols does Azure Load Balancer support?
5. What is a frontend IP configuration?
6. What is a backend pool?
7. What is a load-balancing rule?
8. What is a health probe?
9. What is the difference between a public and an internal Load Balancer?
10. What is the difference between a regional and a cross-region Load Balancer?
11. What is an inbound NAT rule?
12. What is an outbound rule?
13. What is an HA Ports rule?
14. What is the purpose of a Standard Load Balancer?
15. Does Azure Load Balancer automatically scale backend virtual machines?


**Intermediate Questions
**
1. Explain the complete traffic flow through Azure Load Balancer.
2. How does Azure Load Balancer select a backend instance?
3. What is hash-based distribution?
4. What is the five-tuple used in load distribution?
5. How does a health probe determine whether a backend is healthy?
6. What is the difference between TCP, HTTP, and HTTPS health probes?
7. What happens when a backend virtual machine becomes unhealthy?
8. How does session persistence work in Azure Load Balancer?
9. What is the difference between the None, Client IP, and Client IP and protocol distribution modes?
10. Can Azure Load Balancer distribute traffic across virtual machines in different regions?
11. What is the relationship between a frontend port and a backend port?
12. Why might a backend VM fail a health probe even when the VM is running?
13. How do Network Security Groups affect Azure Load Balancer traffic?
14. Why does an inbound load-balancing rule not automatically guarantee outbound internet connectivity?
15. What are the key differences between Azure Load Balancer and Application Gateway?

**
Advanced and Tough Questions**

1. How does Azure Load Balancer maintain flow consistency when traffic is distributed across multiple backend instances?
2. Why might one backend VM receive significantly more traffic than another even when both are healthy?
3. What happens to existing TCP connections when a backend instance becomes unhealthy?
4. How would you design a health probe for a stateful web application?
5. What problems can occur if a health endpoint returns HTTP 200 even when the application cannot serve requests?
6. How would you troubleshoot a scenario where all backend instances are marked unhealthy?
7. How would you troubleshoot a load balancer that is reachable but does not forward traffic to the backend pool?
8. What factors should you consider when choosing between a public and an internal Load Balancer?
9. How would you design a highly available application using Azure Load Balancer across multiple availability zones?
10. How would you design traffic distribution across two Azure regions?
11. Why is hash-based distribution not equivalent to round-robin distribution?
12. How can session persistence affect traffic distribution and backend utilization?
13. What are the limitations of using client-IP-based persistence when many users share a NAT gateway?
14. How would you investigate intermittent connection failures when the health probes appear healthy?
15. What is the role of outbound SNAT in Azure Load Balancer, and what problems can occur when outbound port capacity is exhausted?
16. How would you securely expose a public application while preventing direct, unauthorized access to backend VMs?
17. What considerations are important when using Azure Load Balancer with network virtual appliances?
18. How would you determine whether an application requires Azure Load Balancer or Application Gateway?
19. What is the impact of incorrect probe intervals or failure thresholds on application availability?
20. How would you troubleshoot asymmetric routing or unexpected response-path behavior in a complex network architecture?


**Scenario-Based Questions
**
1. You have three backend VMs behind a public Load Balancer. One VM stops responding. Describe what should happen and how you would verify it.
2. Users can reach the frontend IP, but the application is unavailable. What would you check first?
3. All backend VMs are healthy, but traffic is not evenly distributed. Is this necessarily a problem? Explain.
4. A health probe fails even though the application works when tested manually. What could explain the difference?
5. Your application uses TCP port 443, but the Load Balancer rule forwards traffic to port 80. What problems could occur?
6. A VM has been added to the backend pool but receives no new traffic. How would you troubleshoot it?
7. A business wants to expose an internal API without assigning it a public IP. How would you design the solution?
8. A company runs its application in two Azure regions and wants a global entry point. Which Load Balancer architecture would you consider?
9. A web application requires URL-path-based routing, such as `/api` and `/images`. Would Azure Load Balancer alone be sufficient? Why?
10. Users experience dropped connections whenever a backend VM is restarted. What would you investigate?
11. A backend application is healthy, but its dependent database is unavailable. How should the health endpoint behave?
12. A public Load Balancer works for inbound traffic, but backend VMs cannot access the internet. What could be missing?
13. A security team wants management access to a specific VM without distributing management traffic across all VMs. Which component might be appropriate?
14. After enabling session persistence, one backend becomes overloaded. What might be causing this, and how would you investigate it?
15. Your organization wants to add backend VMs automatically when traffic increases. Which additional Azure capability would you use?


**
Expert-Level Design Questions**

1. Design a highly available three-tier application using Azure Load Balancer. Explain the role of each component.
2. Compare regional Load Balancer, cross-region Load Balancer, and Application Gateway in terms of architecture and use cases.
3. Explain how health-probe configuration can affect failover behavior and application reliability.
4. Design a secure inbound and outbound traffic architecture for a public web application hosted on Azure VMs.
5. How would you diagnose connection failures caused by backend port exhaustion, SNAT limitations, or restrictive network rules?
6. How would you validate load-balancing behavior under high concurrency and uneven client traffic?
7. Explain how availability zones, backend health, autoscaling, and application redundancy work together to improve availability.
8. What design changes would you make if backend instances were stateless versus stateful?
9. How would you distinguish a Load Balancer configuration problem from an application, DNS, routing, or firewall problem?
10. Describe a production incident involving Azure Load Balancer and explain your troubleshooting sequence from symptom to root cause.
