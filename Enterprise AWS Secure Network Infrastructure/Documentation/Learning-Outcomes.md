# Learning Outcomes

This project provided hands-on experience in designing, deploying, securing, and managing a multi-tier AWS cloud infrastructure. It strengthened practical knowledge of AWS networking, compute, storage, identity management, and Linux administration by implementing real-world cloud architecture.

---

# AWS Skills Acquired

## Amazon VPC

- Created and configured a custom Virtual Private Cloud (VPC)
- Planned IP addressing using CIDR blocks
- Designed isolated cloud networking
- Connected multiple AWS resources within the VPC

---

## Subnet Design

Implemented both Public and Private Subnets.

### Public Subnet

- Bastion Host
- Apache Web Server
- NAT Gateway

### Private Subnet

- Private Application Server
- Amazon EBS

Learned how subnet placement affects accessibility and security.

---

## Internet Gateway

Learned how an Internet Gateway enables communication between resources in a public subnet and the internet.

Implemented:

- Internet Gateway creation
- VPC attachment
- Public route configuration

---

## Route Tables

Configured routing for different network paths.

Implemented:

- Public Route Table
- Private Route Table
- Internet Gateway routing
- NAT Gateway routing
- Gateway VPC Endpoint routing
- VPC Peering routing

---

# Compute Services

## Amazon EC2

Learned to:

- Launch EC2 instances
- Configure instance networking
- Connect using SSH
- Deploy an Apache Web Server
- Manage instance security

---

## Bastion Host

Implemented a Bastion Host for secure administration of private resources.

Skills gained:

- Secure SSH architecture
- Administrative access control
- Private server management

---

# Storage

## Amazon EBS

Configured persistent block storage.

Practical tasks completed:

- Attach EBS volume
- Create a filesystem
- Mount the volume
- Configure automatic mounting using `/etc/fstab`
- Verify storage availability

---

## Amazon S3

Configured Amazon S3 for object storage.

Learned:

- Bucket creation
- Secure access from EC2
- Private connectivity using a Gateway VPC Endpoint

---

# Networking

Implemented several AWS networking services.

Skills gained:

- CIDR planning
- Public and Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- VPC Peering
- Gateway VPC Endpoint

---

# Security

Implemented multiple layers of security.

Learned:

- Security Group configuration
- Network ACL configuration
- Bastion Host architecture
- IAM Role-based authentication
- Private subnet isolation
- Least privilege access

---

# Identity and Access Management

Configured IAM Roles for secure communication between EC2 and Amazon S3.

Learned:

- Role-based authentication
- Temporary AWS credentials
- Eliminating hardcoded access keys

---

# Linux Administration

Performed Linux administration tasks on Amazon EC2.

Skills gained:

- Package management
- Service management using `systemctl`
- File editing using `nano`
- SSH administration
- File permission management
- Filesystem management
- Storage mounting

---

# Network Troubleshooting

Resolved real-world networking issues during deployment.

Key troubleshooting experience:

- Diagnosed Apache connectivity issues
- Identified missing Ephemeral Port rules in the Public Network ACL
- Verified Route Table configuration
- Tested Security Group rules
- Validated VPC Peering connectivity
- Confirmed persistent EBS mounting

---

# Practical Experience

This project provided hands-on experience with:

- Designing enterprise network architecture
- Deploying secure cloud infrastructure
- Managing Linux-based EC2 instances
- Configuring persistent storage
- Implementing secure network access
- Establishing private AWS service connectivity
- Connecting multiple VPCs using VPC Peering
- Documenting cloud infrastructure deployments

---

# AWS Services Used

- Amazon VPC
- Amazon EC2
- Amazon EBS
- Amazon S3
- Internet Gateway
- NAT Gateway
- Elastic IP
- Route Tables
- Security Groups
- Network ACLs
- IAM
- Gateway VPC Endpoint
- VPC Peering

---

# Key Takeaways

- Designed and deployed a secure AWS network from scratch.
- Implemented public and private subnet architecture following AWS best practices.
- Secured administrative access using a Bastion Host.
- Configured persistent Amazon EBS storage for Linux instances.
- Enabled private Amazon S3 access using a Gateway VPC Endpoint.
- Established secure communication between two VPCs using VPC Peering.
- Applied Linux administration skills to manage cloud resources.
- Troubleshot and resolved networking issues during deployment.
- Improved understanding of AWS networking, security, and infrastructure design through practical implementation.

---

# Future Improvements

Potential enhancements for this project include:

- Deploying an Application Load Balancer (ALB)
- Configuring Auto Scaling Groups (ASG)
- Hosting a highly available web application across multiple Availability Zones
- Implementing Amazon CloudWatch monitoring and alarms
- Enabling AWS CloudTrail for auditing and governance
- Using AWS Systems Manager Session Manager for administrative access
- Automating infrastructure deployment with AWS CloudFormation or Terraform
- Integrating AWS Backup for automated backup management

---

# Conclusion

This project demonstrates the practical implementation of a secure AWS cloud infrastructure using industry-standard networking and security practices. It combines AWS networking, compute, storage, identity management, and Linux administration into a single hands-on project, providing a strong foundation for entry-level Cloud Engineer and Cloud Support roles.
