# Implementation-of-Static-and-Default-Routing-for-ISP-Failover-in-SBI-Office-Network

Project Title: Implementation of Static and Default Routing for ISP Failover in SBI Office Network

Overview:
This project involved designing and implementing a resilient network architecture for SBI's office, aimed at ensuring uninterrupted internet connectivity through the use of static and default routing protocols. The office required reliable connectivity to handle day-to-day banking operations, making network redundancy a crucial factor. The solution was to connect the office network to two different Internet Service Providers (ISPs), Airtel and Reliance, and implement a failover mechanism.

Objectives:

Ensure continuous internet access by configuring failover between two ISPs.
Use static and default routing to prioritize one ISP while using the other as a backup.
Seamlessly switch to the backup ISP (Reliance) in case of a failure of the primary ISP (Airtel).
Enhance network reliability and minimize downtime without manual intervention.
Project Implementation:

Network Topology:
The network consisted of multiple office PCs connected to a central switch, which was in turn connected to a router. The router had two interfaces: one connected to Airtel (192.168.3.2) and the other to Reliance (192.168.4.2). Airtel was configured as the primary internet provider, and Reliance acted as the backup in case Airtel went down.

Default Routing Configuration:
Default routes were configured for both ISPs, with different metrics assigned to prioritize Airtel:

Airtel: ip route 0.0.0.0 0.0.0.0 192.168.3.2 10
Reliance: ip route 0.0.0.0 0.0.0.0 192.168.4.2 50
The metric value of 10 for Airtel made it the preferred route, while Reliance, with a metric of 50, would only be used if Airtel was unavailable.

Static Routing for Specific Services:
Static routes were configured for critical services like Google DNS (8.8.8.8) to ensure they always had a direct, reliable path. This was necessary for maintaining DNS resolution and other network services even if the default route changed due to ISP failure.

Command: ip route 8.8.8.8 255.255.255.255 192.168.24.4.
Failover Mechanism:
After configuring the default and static routes, I tested the failover by simulating a failure on the Airtel link. This was achieved by shutting down Airtel’s interface using the command:

shutdown interface f0/0.
Once Airtel was down, the router automatically switched traffic to Reliance (192.168.4.2) without any user intervention. The switch was validated by using traceroute and verifying that traffic was rerouted through Reliance's gateway.

Testing and Validation:
To ensure proper failover, I ran tests by initiating a traceroute to Google's public DNS (8.8.8.8). Initially, traffic flowed through Airtel, but when Airtel's link was manually shut down, the traffic seamlessly switched to Reliance. This validated the correct implementation of the failover mechanism and confirmed that the network would remain functional even if the primary ISP failed.

Results:

The project successfully ensured uninterrupted internet connectivity for SBI’s office. The failover between ISPs was automatic, requiring no manual intervention when Airtel went down.
The use of default routes with different metrics allowed efficient routing of traffic through the preferred ISP (Airtel), while ensuring that Reliance was available as a backup in case of any issues.
By configuring static routes for critical services like Google DNS, I ensured that key network functions would continue to work reliably, even during a failover event.
This implementation improved the network’s resilience, allowing SBI’s office to maintain high availability for critical banking operations.
Key Takeaways:

The project demonstrated my ability to work with routing protocols, specifically static and default routing, to build fault-tolerant network solutions.
I gained experience in configuring routers for real-time failover between ISPs and testing complex network behaviors using tools like traceroute.
The project highlights my practical skills in networking, including configuring route metrics, IP addressing, and troubleshooting failover scenarios to ensure network uptime.
