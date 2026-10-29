# Azure Front Door Load Balancer 

## Set 1: Basic-Level Questions

1. What is Azure Front Door?
2. Why is Azure Front Door used?
3. Is Azure Front Door a Layer 4 or Layer 7 load-balancing service?
4. What is global load balancing?
5. What is the difference between global and regional load balancing?
6. What is an Azure Front Door profile?
7. What is an endpoint in Azure Front Door?
8. What is an origin?
9. What is an origin group?
10. What is a route in Azure Front Door?
11. What is an edge location or Point of Presence (POP)?
12. What is the Microsoft global edge network?
13. What is a custom domain in Azure Front Door?
14. What is the purpose of a health probe?
15. What is the difference between HTTP and HTTPS?
16. What is TLS termination?
17. What is a Content Delivery Network (CDN)?
18. What is edge caching?
19. What is a Web Application Firewall (WAF)?
20. What is the difference between Azure Front Door and Azure Load Balancer?

## Set 2: Intermediate-Level Questions

1. How does Azure Front Door distribute traffic across multiple regions?
2. How does Azure Front Door select the best origin for an incoming request?
3. What is latency-based routing?
4. What is priority-based routing?
5. What is weighted routing?
6. What is session affinity in Azure Front Door?
7. What happens when an origin becomes unhealthy?
8. How do health probes work in Azure Front Door?
9. What is the difference between an origin and an endpoint?
10. Can Azure Front Door distribute traffic to origins outside Azure?
11. How does Azure Front Door support high availability?
12. How does Azure Front Door improve website performance?
13. What is the difference between static and dynamic content delivery?
14. What is a cache hit and a cache miss?
15. How do you configure HTTP-to-HTTPS redirection?
16. How does Azure Front Door handle custom domains and SSL/TLS certificates?
17. What is the purpose of the Rules Engine?
18. How can Azure Front Door route different URL paths to different origins?
19. What is the difference between Azure Front Door Standard and Premium?
20. How does Azure Front Door differ from Azure Application Gateway?

## Set 3: Advanced Technical Questions

1. Explain the complete request flow from a user's browser to a backend application through Azure Front Door.
2. How does Azure Front Door determine origin eligibility using health probes, priority, latency, and weights?
3. How does the latency sensitivity setting influence origin selection?
4. What happens when multiple origins have the same priority but different weights?
5. What happens when the lowest-latency origin becomes unhealthy?
6. How does session affinity affect global traffic distribution?
7. How would you design an active-active multi-region architecture using Azure Front Door?
8. How would you design an active-passive disaster recovery architecture using Azure Front Door?
9. How would you configure Azure Front Door to distribute approximately 80% of eligible traffic to one origin and 20% to another?
10. How would you gradually migrate production traffic from one Azure region to another?
11. How does Azure Front Door handle TLS connections between clients, edge locations, and origins?
12. What are the security risks of disabling origin certificate name validation?
13. How would you configure a custom domain with a managed TLS certificate?
14. How does Azure Front Door Premium integrate with Azure Private Link?
15. How would you prevent users from bypassing Azure Front Door and directly accessing the origin?
16. How does Azure Front Door caching interact with Cache-Control headers?
17. How can query-string configuration affect cache behavior?
18. What are the risks of caching authenticated or personalized API responses?
19. How would you troubleshoot a low cache-hit ratio?
20. How would you investigate unexpected origin selection in a multi-region deployment?

## Set 4: Scenario-Based Interview Questions

1. Your application is hosted in East US and West Europe. How would you configure Azure Front Door to route users to an appropriate healthy origin?
2. Your primary application region becomes unavailable. How would Azure Front Door redirect traffic to a secondary region?
3. Users in India report high latency while European users experience normal performance. How would you investigate?
4. Your application works when accessed directly through the origin URL but fails through Azure Front Door. What would you check?
5. Azure Front Door is returning HTTP 502 errors. How would you troubleshoot the issue?
6. Your application returns HTTP 503 errors after a regional outage. What could be causing the problem?
7. Your application returns intermittent HTTP 504 errors. How would you identify whether the issue is at the edge, network, or origin?
8. Your health probe reports an origin as unhealthy even though the website loads directly. What might explain this?
9. You want `/api/*` requests to reach an API origin and `/images/*` requests to reach a static content origin. How would you configure the routing?
10. You want to redirect all HTTP traffic to HTTPS without creating redirect loops. How would you implement and test this?
11. Your company wants to migrate users gradually from an old backend to a new backend. How would you use weighted routing?
12. After enabling WAF prevention mode, legitimate customers receive HTTP 403 errors. How would you investigate?
13. Users receive outdated CSS and JavaScript files after a deployment. How would you troubleshoot caching?
14. Your application uses server-local sessions and users are unexpectedly logged out after failover. How would you address this?
15. Your company wants to expose an application globally without making its origin publicly accessible. What architecture would you recommend?
16. Your application experiences a sudden traffic spike during a global product launch. How would you prepare Front Door and the origins?
17. You need to host multiple websites using different custom domains behind a single Azure Front Door profile. How would you design the configuration?
18. Your custom domain works over HTTP but fails over HTTPS. What would you investigate?
19. A regional origin becomes unhealthy during a deployment. How would you minimize user impact?
20. Your Azure Front Door traffic distribution does not match the configured origin weights. What factors would you examine?

## Set 5: Security and WAF Questions

1. What security features are available in Azure Front Door?
2. How does Azure Front Door WAF protect web applications?
3. What is the difference between WAF detection mode and prevention mode?
4. What are managed WAF rules?
5. What are custom WAF rules?
6. How can Azure Front Door help protect against SQL injection and cross-site scripting attacks?
7. What is rate limiting, and how can it help protect an application?
8. What is bot protection in Azure Front Door?
9. How would you investigate a WAF false-positive detection?
10. How would you design a WAF exclusion without unnecessarily weakening security?
11. How does Azure Front Door help mitigate DDoS attacks?
12. What is origin bypass, and why is it a security risk?
13. How would you restrict direct access to an Azure App Service origin?
14. What is the role of Azure Private Link in Front Door Premium?
15. How would you secure traffic between Azure Front Door and a backend origin?
16. How would you implement security controls for multiple applications sharing one Front Door profile?
17. What security risks can arise from incorrect request-header rewrite rules?
18. How would you monitor suspicious traffic patterns using Front Door diagnostic logs?
19. How would you investigate a sudden increase in WAF-blocked requests?
20. How would you combine Azure Front Door WAF with application-level authentication and authorization?

## Set 6: Architecture and Design Questions

1. How would you design a globally available e-commerce application using Azure Front Door?
2. How would you combine Azure Front Door with Azure Application Gateway?
3. How would you combine Azure Front Door with Azure App Service deployments across multiple regions?
4. How would you design a global API architecture using Azure Front Door and Azure API Management?
5. How would you integrate Azure Front Door with Azure Kubernetes Service (AKS)?
6. How would you design a highly available architecture that can survive a complete Azure regional outage?
7. What are the differences between active-active and active-passive architectures?
8. How would you ensure data consistency across multiple application regions?
9. How would you handle user sessions in a multi-region active-active deployment?
10. How would you design global routing when different regions have different backend capacities?
11. How would you use Azure Front Door for blue-green deployments?
12. How would you design a canary release strategy using weighted routing?
13. How would you implement a disaster recovery plan with defined RTO and RPO targets?
14. What are the advantages and disadvantages of using a single Front Door profile for multiple applications?
15. When would you choose separate Front Door profiles for different business applications?
16. How would you design secure private-origin connectivity for a globally accessible application?
17. How would you configure global traffic routing for an application with regional data residency requirements?
18. How would you plan origin capacity to handle failover traffic from another region?
19. How would you choose between Azure Front Door, Azure Traffic Manager, and Azure Application Gateway?
20. How would you design an architecture that combines global routing, regional Layer 7 routing, and internal Layer 4 load balancing?

## Set 7: Troubleshooting and Production Support Questions

1. What steps would you follow when Azure Front Door returns HTTP 502 Bad Gateway?
2. How would you troubleshoot HTTP 503 Service Unavailable errors?
3. How would you troubleshoot HTTP 504 Gateway Timeout errors?
4. How would you identify whether an issue originates from Azure Front Door or the backend application?
5. How would you troubleshoot origin health probe failures?
6. How would you investigate a TLS certificate hostname mismatch?
7. How would you troubleshoot incorrect custom-domain DNS configuration?
8. How would you investigate unexpected HTTP-to-HTTPS redirect loops?
9. How would you troubleshoot inconsistent routing behavior across origins?
10. How would you determine whether a Rules Engine configuration is causing request failures?
11. How would you investigate increased latency after deploying a new Front Door route?
12. How would you troubleshoot an origin that is accessible publicly but not through Private Link?
13. How would you investigate a sudden decrease in cache-hit ratio?
14. How would you troubleshoot missing or incomplete diagnostic logs?
15. How would you identify whether WAF is blocking legitimate requests?
16. How would you investigate a production outage affecting only one custom domain?
17. How would you troubleshoot a situation where one origin receives nearly all the traffic despite equal weights?
18. How would you determine whether an origin timeout is caused by the application, database, or network?
19. How would you validate that automatic failover is working as expected?
20. How would you safely restore traffic to a recovered primary origin?

## Set 8: Expert-Level and Tough Questions

1. Explain how Azure Front Door evaluates origin health, priority, latency sensitivity, and weight when selecting an origin.
2. What are the limitations of using weighted routing for precise traffic percentage control?
3. How would you investigate inconsistent origin selection caused by session affinity and changing health states?
4. How would you design an architecture that remains available when an entire region and its dependent data services fail?
5. How would you implement zero-downtime deployments across multiple Azure regions?
6. How would you prevent stale or sensitive content from being served through edge caching?
7. How would you design and validate origin authentication and origin bypass protection?
8. How would you handle long-running HTTP requests and connection timeouts in Azure Front Door?
9. How would you investigate an intermittent TLS handshake failure between Front Door and an origin?
10. How would you design a migration from Azure Front Door Classic to Standard or Premium while minimizing downtime?
11. How would you choose between Front Door Standard and Premium based on security, networking, and cost requirements?
12. How would you measure the real performance improvement delivered by Azure Front Door?
13. How would you design monitoring to distinguish edge errors, origin errors, WAF blocks, and application errors?
14. How would you implement automated regional failover testing without disrupting production traffic?
15. How would you design a multi-region application where write operations must remain consistent during failover?
16. How would you ensure that disaster recovery does not violate data residency or compliance requirements?
17. How would you investigate routing differences caused by latency sensitivity settings versus origin weights?
18. How would you build an Infrastructure as Code deployment pipeline for Azure Front Door with safe rollbacks?
19. How would you optimize Azure Front Door cost for a globally distributed, high-traffic application?
20. How would you perform a complete architecture review of Azure Front Door covering reliability, security, performance, operations, and cost?

## Set 9: Azure Front Door vs Other Load Balancing Services

1. What is the difference between Azure Front Door and Azure Load Balancer?
2. What is the difference between Azure Front Door and Azure Application Gateway?
3. What is the difference between Azure Front Door and Azure Traffic Manager?
4. How does DNS-based routing differ from HTTP reverse-proxy routing?
5. Why can Azure Front Door perform URL-based routing while Azure Load Balancer cannot?
6. What are the advantages of Azure Front Door over a regional Application Gateway for global applications?
7. When would Azure Traffic Manager be more appropriate than Azure Front Door?
8. When would Azure Load Balancer be more appropriate than Azure Front Door?
9. What is the difference between edge caching in Azure Front Door and backend load balancing in Application Gateway?
10. Can Azure Front Door and Azure Application Gateway be used together, and what benefits and trade-offs would that introduce?
11. How do health checks differ between Azure Front Door and Azure Load Balancer?
12. How do global failover mechanisms differ between Azure Front Door and Azure Traffic Manager?
13. How does Azure Front Door handle HTTP/HTTPS traffic compared with Azure Load Balancer's TCP/UDP traffic handling?
14. What are the security differences between Front Door WAF and Application Gateway WAF?
15. How would you select the appropriate Azure load-balancing service for a new enterprise application?

## Set 10: Real-World Production Challenge Questions

1. Your application serves 10 million users across five continents. Design a globally available Azure Front Door architecture that balances latency, security, availability, and cost.
2. Your company has three regional origins with different capacities. Design a routing strategy that considers origin health, latency, and capacity.
3. A regional outage occurs while the backup region is already operating at 80% capacity. How would you prevent the failover from overwhelming the backup?
4. During a product launch, Front Door request volume increases tenfold, but origin CPU usage remains low while users experience high latency. How would you investigate?
5. Your company must migrate a critical application from Front Door Classic to Premium with minimal downtime. What migration, validation, and rollback strategy would you design?
6. Your organization requires private origins, WAF protection, end-to-end TLS, and global failover. Design the complete architecture and explain its limitations.
7. A WAF policy blocks a critical payment API only during peak traffic. How would you identify and resolve the issue without removing essential security controls?
8. Your application is active-active across two regions, but users lose shopping-cart data after regional failover. How would you redesign the session and data architecture?
9. A new deployment causes a sudden increase in origin errors, but Front Door health probes continue to report healthy origins. How would you improve the health-check and monitoring strategy?
10. Your application must meet a 99.99% availability objective. How would you evaluate whether the Front Door architecture, origin infrastructure, data layer, and operational processes can support that objective?
