# AWS VPC Peering Project

## Project Overview

This project demonstrates private network communication between two separate Amazon Virtual Private Clouds (VPCs) using AWS VPC Peering. Route tables and security groups were configured to allow controlled communication between EC2 instances in both VPCs.

## Objectives

- Create two VPCs with different IPv4 CIDR blocks.
- Configure public and private subnets.
- Establish an active VPC Peering connection.
- Configure routes between the two VPCs.
- Launch EC2 instances and configure security groups.
- Access private instances through a bastion host.
- Verify connectivity using ICMP ping tests.

## AWS Services and Technologies

- Amazon VPC
- VPC Peering
- Amazon EC2
- Route Tables
- Security Groups
- Internet Gateway
- Amazon Linux 2023
- SSH and ICMP

## Network Configuration

| Resource | Configuration |
|---|---|
| AWS Region | Asia Pacific (Sydney) — `ap-southeast-2` |
| VPC A | `ewb-vpc-a` — `10.10.0.0/16` |
| VPC B | `ewb-vpc-b` — `10.20.0.0/16` |
| VPC A Public Subnet | `10.10.1.0/24` |
| VPC A Private Subnet | `10.10.2.0/24` |
| VPC B Private Subnet | `10.20.1.0/24` |
| VPC Peering Connection | `ewb-a-b-peer` |

## EC2 Instances

| Instance | Private IP | Purpose |
|---|---|---|
| `ewb-bastion` | `10.10.1.10` | Bastion host |
| `ewb-app-a` | `10.10.2.10` | Application instance in VPC A |
| `ewb-app-b` | `10.20.1.10` | Application instance in VPC B |

## Routing and Security

Routes were configured in the VPC route tables to direct traffic for the remote VPC CIDR through the VPC Peering connection.

Security groups restricted SSH and ICMP traffic to specified source addresses. The bastion host was used to access the private application instances.

## Testing and Results

### Test 1: Application A to Application B

Command: `ping -c 4 10.20.1.10`

**Result:** Successful — 4 packets received, 0% packet loss.

### Test 2: Application B to Application A

Command: `ping -c 4 10.10.2.10`

**Result:** Successful — 4 packets received, 0% packet loss.

### Test 3: Security Group Verification

The ICMP rule allowing traffic from Application A was temporarily removed from Application B's security group. The ping failed. After the rule was restored, connectivity succeeded again.

## Project Evidence

This repository contains the project report and screenshots documenting the VPC configuration, peering status, route tables, EC2 instances, security group rules, and connectivity tests.

## Conclusion

The project successfully demonstrated private communication between two AWS VPCs using VPC Peering. The connectivity tests verified communication in both directions, while the security group test demonstrated the importance of controlled network access.

## Repository Contents

- Project report PDF
- AWS configuration screenshots
- VPC Peering connectivity test evidence

## Cost Management

The EC2 instances were stopped after testing. EBS volumes were retained so the environment can be used again. AWS storage and other applicable resource charges may continue while resources remain allocated.
