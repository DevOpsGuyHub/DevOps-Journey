# Azure Application Gateway & Load Balancer
## Set 1: Basic-Level Questions

1. What is Azure Application Gateway?
2. What is Azure Load Balancer?
3. What is the main difference between Azure Application Gateway and Azure Load Balancer?
4. What is Layer 4 load balancing?
5. What is Layer 7 load balancing?
6. What is a frontend IP configuration?
7. What is a backend pool?
8. What is a listener in Application Gateway?
9. What is a routing rule?
10. What is a health probe?
11. What is a backend setting in Application Gateway?
12. What is the purpose of a frontend port?
13. What is the difference between a public and private frontend IP?
14. What is a virtual network in Azure?
15. Why does Application Gateway require a dedicated subnet?
16. What is the purpose of a Network Security Group (NSG)?
17. What is a public Load Balancer?
18. What is an internal Load Balancer?
19. What is the difference between inbound and outbound traffic?
20. What happens when a backend server becomes unhealthy?

## Set 2: Intermediate-Level Questions

1. How does Azure Application Gateway distribute incoming HTTP and HTTPS requests?
2. How does Azure Load Balancer distribute TCP and UDP traffic?
3. What is the difference between a listener and a backend pool?
4. What is the difference between a health probe and a routing rule?
5. What is path-based routing in Application Gateway?
6. What is multi-site hosting?
7. How can one Application Gateway host multiple websites?
8. What is TLS termination, and why is it useful?
9. What is end-to-end TLS encryption?
10. What is the difference between HTTP and HTTPS listeners?
11. What is Web Application Firewall (WAF)?
12. What is the difference between WAF and a Network Security Group?
13. What is session affinity, and when would you use it?
14. What is autoscaling in Application Gateway?
15. What is zone redundancy?
16. What is the purpose of custom health probes?
17. How does Application Gateway handle requests when multiple backend servers are available?
18. What is the difference between URL path-based routing and host-based routing?
19. How do you configure Application Gateway to redirect HTTP traffic to HTTPS?
20. How can you troubleshoot a backend health status showing as Unhealthy?
21. Can an Azure Load Balancer route traffic based on URL paths?
22. What is the difference between a Load Balancer rule and an inbound NAT rule?
23. What is a floating IP in Azure Load Balancer?
24. How does a Load Balancer health probe affect traffic distribution?
25. What are the key differences between Application Gateway v2 and Azure Load Balancer?

## Set 3: Advanced and Tough Questions

1. Explain the complete request flow from a client to an application hosted behind Azure Application Gateway.
2. How would you design a highly available web application using Application Gateway, Virtual Machine Scale Sets, and multiple Availability Zones?
3. An Application Gateway listener receives HTTPS traffic, but the backend uses HTTP. Explain how the request flows and what security considerations apply.
4. What happens if the frontend listener is healthy but all backend servers are unhealthy?
5. How would you troubleshoot an Application Gateway returning HTTP 502 errors?
6. How would you troubleshoot intermittent HTTP 504 Gateway Timeout errors?
7. An Application Gateway backend is marked Unhealthy even though the application works directly. What could be the causes?
8. How would you configure path-based routing for `/api`, `/images`, and `/admin` to different backend pools?
9. How would you host `app.example.com` and `api.example.com` on a single Application Gateway?
10. How would you configure end-to-end TLS when the backend servers use certificates signed by an internal certificate authority?
11. What issues can occur if the backend certificate's hostname does not match the hostname used for backend TLS validation?
12. How would you securely expose a public web application while keeping backend virtual machines private?
13. What happens when Application Gateway reaches its configured maximum capacity?
14. How would you decide between fixed capacity and autoscaling?
15. How would you design a deployment to minimize downtime when updating backend servers?
16. How would you troubleshoot a case where HTTP works but HTTPS fails?
17. How can routing rules, rewrite rules, and redirect rules interact, and what problems can incorrect configurations cause?
18. How would you investigate a sudden increase in Application Gateway latency?
19. How would you troubleshoot an Application Gateway that cannot reach its backend because of NSG or user-defined route restrictions?
20. How would you determine whether a 403 response originates from WAF or from the backend application?
21. How would you configure WAF detection and prevention modes, and what are the trade-offs?
22. How would you investigate false-positive WAF detections without weakening the application's security?
23. What are the architectural implications of placing Application Gateway and Azure Load Balancer in the same request path?
24. How would you choose between Application Gateway, Azure Load Balancer, and Azure Front Door for a global web application?
25. How would you design a solution that needs global routing, regional Layer 7 routing, and internal TCP load balancing?

## Set 4: Scenario-Based Interview Questions

1. You have three web servers behind an Azure Load Balancer. One server stops responding. How should the Load Balancer behave?
2. You need to route `/customer` traffic to one backend and `/employee` traffic to another. Which Azure service would you choose, and why?
3. Your company hosts ten websites on different domains but wants to minimize gateway infrastructure. How would you design the solution?
4. Users can access your application through its public IP, but access through the domain name fails. How would you investigate?
5. Your application works from inside the virtual network but is inaccessible from the internet. What would you check?
6. After enabling WAF prevention mode, legitimate users begin receiving 403 errors. How would you investigate and resolve the issue?
7. Traffic increases significantly during business hours. How would you ensure that the gateway and backend infrastructure scale appropriately?
8. A backend application requires the original client IP address for logging. How would you make that information available?
9. A deployment requires the same user to remain connected to the same backend server. Which feature might help, and what are its limitations?
10. You need to expose a web application publicly while keeping the API backend accessible only through private networking. How would you design the architecture?
11. An Application Gateway is returning 502 errors after a backend certificate update. What would you investigate?
12. A Load Balancer distributes TCP traffic successfully, but your application needs host-header-based routing. What architectural change would you make?
13. Your organization needs a private IP endpoint for an internal application used by several virtual machines. Which Load Balancer configuration would you consider?
14. A health probe reports success, but users still receive application errors. What could explain this?
15. You need to protect a web application from common SQL injection and cross-site scripting attacks. Which Azure features would you consider?
16. Your application must remain available if an entire Availability Zone fails. What design considerations are necessary?
17. You have a regional web application today but expect users worldwide in the future. How might your architecture evolve?
18. After changing an NSG rule, Application Gateway can no longer reach its backend pool. How would you identify the blocked traffic?
19. The backend application is healthy, but requests to `/api/orders` return 404 while `/` works. How would you isolate the issue?
20. You need both Layer 7 routing to web servers and Layer 4 load balancing for a database or TCP service. How would you combine Azure networking services?

## Set 5: Expert-Level Design and Troubleshooting

1. Compare Azure Application Gateway, Azure Load Balancer, Azure Front Door, and Azure Traffic Manager in terms of routing layer, scope, protocols, and typical use cases.
2. Explain the difference between load-balancing algorithms and session persistence. How can these affect application performance?
3. How would you investigate asymmetric routing or unexpected connection failures in a complex Azure network?
4. How would you plan subnet sizing and IP address capacity for an autoscaling Application Gateway deployment?
5. What metrics and diagnostic logs would you use to identify whether latency originates at the gateway or backend?
6. How would you design a blue-green deployment strategy using Application Gateway?
7. What are the risks of relying on session affinity for a horizontally scaled application?
8. How would you handle WebSocket or long-running connections in a gateway-based architecture?
9. How would you design certificate rotation for frontend HTTPS listeners and backend TLS connections?
10. What are the security implications of allowing direct public access to backend servers behind Application Gateway?
11. How would you diagnose intermittent failures caused by backend connection limits or exhausted application resources?
12. How would you choose between a single shared Application Gateway and multiple gateways for separate applications or teams?
13. How would you assess the cost, security, availability, and operational trade-offs between Application Gateway and Azure Load Balancer?
14. How would you design a multi-region architecture that combines global entry-point routing with regional Layer 7 inspection?
15. What would your end-to-end troubleshooting workflow look like for a production outage involving DNS, TLS, Application Gateway, NSGs, routing, and backend application health?
