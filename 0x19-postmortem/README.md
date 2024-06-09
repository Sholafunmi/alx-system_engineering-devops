Postmortem Report



Issue Summary

Duration of Outage: June 7, 2024, 02:00pm - 6:30pm UTC

Impact: 
The outage affected the primary web application service, resulting in 50% of users experiencing slow load times and intermittent 500 Internal Server Error responses. Approximately 30% of users were unable to access the service entirely during peak times.

Root Cause:
A misconfiguration in the load balancer's settings caused an uneven distribution of traffic, leading to server overload and subsequent crashes.


Timeline:

14:00 UTC:  Issue detected by monitoring alert indicating increased error rates and response times.
14:05 UTC:** Initial investigation began, engineers examined server logs and application performance metrics.
14:20 UTC: Assumed root cause was a database performance issue, escalated to the Database Team.
14:45 UTC: Database Team reported no anomalies, redirected focus to application server performance.
15:10 UTC: Suspected a recent deployment might be causing memory leaks, deployment rollback initiated.
15:30 UTC: Rollback completed, but issue persisted; escalated to the Network Operations Team.
16:00 UTC: Network Operations Team identified uneven traffic distribution across servers.
16:15 UTC: Load balancer settings reviewed, found misconfiguration causing traffic routing issues.
16:45 UTC: Applied correct load balancer configuration; gradual improvement observed.
17:30 UTC: Monitoring confirmed system stability, error rates back to normal.
18:30 UTC: Incident officially declared resolved after a sustained period of stability.


Root Cause and Resolution

Root Cause:The root cause of the issue was an incorrect configuration in the load balancer. The load balancer was set to route 80% of incoming traffic to a single server instead of distributing it evenly across all available servers. This led to the overloaded server failing under high traffic conditions, causing slow load times and errors for a significant portion of users.

Resolution: The misconfiguration was corrected by updating the load balancer settings to ensure even traffic distribution. Specifically, the weight distribution parameters were adjusted to balance the traffic load correctly across all servers. After applying the changes, the load was monitored to ensure even distribution, and the system's performance returned to normal.


Corrective and Preventative Measures

Improvements and Fixes:
Improved Load Balancer Configuration Management:Implement stricter configuration management processes to avoid manual errors.
Enhanced Monitoring: Set up more granular monitoring of load balancer traffic distribution and server loads.
Regular Configuration Audits:** Conduct regular audits of load balancer settings and configurations.

Tasks to Address the Issue:
1. Patch Load Balancer Configuration: Immediately apply the corrected configuration to all load balancers.
2. Add Monitoring on Load Balancer Traffic Distribution: Implement detailed monitoring and alerting on the traffic distribution metrics of the load balancer.
3. Conduct Configuration Management Training:Provide additional training for engineers on proper load balancer configuration management.
4. Implement Configuration Version Control: Use a version control system for managing load balancer configurations to track changes and facilitate rollbacks if needed.
5. Perform Regular Load Tests: Schedule and perform regular load testing to identify potential bottlenecks and configuration issues before they impact users.

By addressing these corrective and preventative measures, we aim to mitigate the risk of similar incidents occurring in the future and ensure the reliability and stability of our web application services.

