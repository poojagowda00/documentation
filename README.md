# documentation
Creating an Application Load Balancer (ALB) and configuring it with multiple target groups can significantly enhance application scalability and reliability.

Instance Setup: Launch four EC2 instances with private subnets, placing two instances in subnet 1A and the remaining two in subnets 1B and 1C. Ensure proper userdata configuration for each instance.

Target Group Creation: Create three target groups: Home Page: HTTP 80, health check /homepage/, add all instances. Movies: HTTP 80, health check /movies/, add movies server only. Shows: HTTP 80, health check /shows/, add shows server only.

Load Balancer Configuration: Create an ALB (Internet-facing) in the VPC, selecting the public subnets and appropriate security group. Configure two listeners: HTTP (80) and HTTPS (443). Selecting the SSL certificate for domain.

Route 53 Setup: Create a Route 53 record pointing to the ALB.

HTTP to HTTPS Redirection: Configure HTTP to HTTPS redirection: Create a rule to redirect HTTP (80) traffic to HTTPS (443). Ensure proper HTTPS redirection for all incoming traffic.

Path-Based Routing: Implement path-based routing for different content: Create rules to direct traffic based on paths (e.g., /movies/, /shows/). Ensure each rule forwards traffic to the corresponding target group.
