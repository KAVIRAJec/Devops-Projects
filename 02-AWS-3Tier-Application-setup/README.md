# AWS 3-Tier Application Setup

## Migration Steps: Local Vagrant to AWS Cloud

Below are the steps followed to migrate the 3-tier application from a local Vagrant/VirtualBox environment to AWS cloud infrastructure:

1. **Created Security Groups and Key Pairs**
   - Set up security groups for application, backend, and load balancer layers to control network access.
   - Generated key pairs for secure SSH access to EC2 instances.

2. **Launched EC2 Instances**
   - Deployed EC2 instances for each component: Tomcat application server, database (DB), Memcached (MC), and RabbitMQ (RMQ).

3. **Configured Private Hosted Zone**
   - Created a private hosted zone in Route 53 to enable internal DNS-based communication between instances (e.g., `db01`, `mc01`, etc.).

4. **Deployed Application Artifacts**
   - Built the application artifact locally.
   - Created an S3 bucket and uploaded the artifact using AWS CLI.
   - SSHed into the app server, installed necessary configurations, and downloaded the artifact from S3 using the instance's IAM role.

5. **Set Up Load Balancer**
   - Established an Elastic Load Balancer (ELB) for the application tier.
   - Configured the load balancer's DNS name as a CNAME record in the domain's DNS settings.

6. **Configured Auto Scaling Groups**
   - Created auto scaling groups to ensure high availability and scalability for the application servers.

---

## Architecture Diagram

![AWS 3-Tier Architecture](AWS%20Lift&Shift%20project.png)

---
