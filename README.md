# AWS Self-Healing Infrastructure with EC2 Auto Scaling and Elastic Load Balancing

## Project Overview

Built an AWS infrastructure designed to automatically replace unhealthy EC2 instances using an Auto Scaling Group integrated with an Elastic Load Balancer and target group health checks.

The goal was to reduce manual intervention, maintain application availability, and understand how AWS handles instance health monitoring and automatic recovery.

## Architecture

**Traffic flow:**

`Internet → Internet Gateway → Route Table → Load Balancer → Target Group → EC2 Instances`

The EC2 instances are managed by an Auto Scaling Group that maintains the desired capacity and replaces instances when they become unhealthy.

## AWS Services Used

- **Amazon VPC** — Created the networking environment.
- **Subnets** — Configured subnets for the infrastructure.
- **Internet Gateway** — Enabled internet connectivity for the VPC.
- **Route Tables** — Configured network routing.
- **Security Groups** — Configured inbound access rules for SSH and HTTP as required.
- **EC2 Launch Template** — Defined the instance configuration and user-data bootstrap script.
- **Amazon EC2** — Hosted the application instances.
- **EC2 Auto Scaling** — Automatically replaced unhealthy instances and maintained the configured capacity.
- **Elastic Load Balancing** — Distributed incoming traffic to registered targets.
- **Target Groups** — Registered EC2 instances and used health checks to assess application availability.
- **AWS Application Recovery Controller** — Explored recovery-related capabilities.

## Auto Scaling Configuration

| Setting | Value |
|---|---:|
| Minimum capacity | 1 instance |
| Desired capacity | 2 instances |
| Maximum capacity | 2 instances |
| Instance management | Automatic replacement of unhealthy instances |
| Launch configuration | EC2 Launch Template |

The Auto Scaling Group was configured to maintain between one and two instances, with a desired capacity of two.

## Implementation Steps

1. Created the VPC networking components, including subnets, an Internet Gateway, and route tables.
2. Created target groups and configured a load balancer.
3. Created security groups and configured inbound rules.
4. Built an EC2 Launch Template with instance settings, security group configuration, and a basic user-data script for SSH/HTTP setup.
5. Created an Auto Scaling Group using the Launch Template.
6. Configured minimum, desired, and maximum capacity.
7. Connected the Auto Scaling Group to the load balancer's target group.
8. Explored target registration and load balancer health checks.
9. Configured instance maintenance policies governing how instances are replaced during certain updates or replacement operations.
10. Explored AWS Application Recovery Controller and its role in recovery-oriented architectures.

## Self-Healing Behaviour

The intended recovery workflow is:

1. An EC2 instance becomes unhealthy.
2. Health checks detect the unhealthy target, provided the Auto Scaling Group is configured to use the relevant load balancer health checks.
3. Auto Scaling identifies the unhealthy instance.
4. The unhealthy instance is terminated and replaced with a new instance.
5. The replacement launches using the configured Launch Template.
6. The new instance starts its bootstrap process and becomes available after passing the required health checks.

This reduces the need for manual instance replacement.

**Important:** Replacement is automatic, but it is not guaranteed to complete in milliseconds. Launching, bootstrapping, registering, and passing health checks can take longer. During recovery, application capacity may temporarily decrease.

## Challenges and Troubleshooting

During implementation, I worked through networking, security group rules, target group registration, and load balancer health checks.

This helped me understand that successful EC2 provisioning alone does not guarantee application availability. Networking, security rules, application configuration, target registration, and health checks must work together.

## Skills Demonstrated

- AWS networking fundamentals
- VPC, subnet, route table, and Internet Gateway configuration
- EC2 provisioning with Launch Templates
- Auto Scaling Group capacity management
- Load balancing and target health checks
- Security group configuration
- User-data bootstrap scripting
- Infrastructure troubleshooting
- High availability and self-healing architecture concepts

## Future Improvements

- Add an architecture diagram.
- Capture screenshots of the VPC, Launch Template, Auto Scaling Group, and target group health.
- Test unhealthy-instance replacement and document the observed recovery time.
- Add CloudWatch monitoring and alarms.
- Automate the infrastructure using Terraform or AWS CloudFormation.
- Review SSH access restrictions and follow least-privilege security practices.

## Project Status

**Hands-on learning project.** The architecture and implementation notes are based on the resources configured during the exercise. Further validation and documentation of recovery testing will strengthen the project evidence.

