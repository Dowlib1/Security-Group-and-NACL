# AWS Security Group and NACL Mini Project

## Project Overview

This project demonstrates hands-on experience with the configuration of AWS Security Groups and Network Access Control Lists (NACLs).  
You will learn how to secure your AWS infrastructure by managing inbound and outbound traffic rules, applying layered network security, and troubleshooting access issues.  
The project uses a sample IP address (`50.18.32.11`) for HTTP access to illustrate practical scenarios.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Step-by-Step Guide](#step-by-step-guide)
   - [1. Launch an EC2 Instance](#1-launch-an-ec2-instance)
   - [2. Configure Security Group](#2-configure-security-group)
   - [3. Configure Network ACL](#3-configure-network-acl)
   - [4. Testing Access](#4-testing-access)
   - [5. Troubleshooting](#5-troubleshooting)
4. [Best Practices](#best-practices)
5. [Conclusion](#conclusion)

---

## Introduction

AWS Security Groups and NACLs are essential for protecting your cloud resources.  
Security Groups act as virtual firewalls for your EC2 instances, while NACLs operate at the subnet level, providing an additional layer of security.  
This documentation provides a step-by-step guide with screenshots to help you understand and implement these features.

---

## Prerequisites

- An AWS account
- Basic knowledge of AWS Management Console
- EC2 instance launched in a VPC

---

## Step-by-Step Guide

### 1. Launch an EC2 Instance

- In the AWS Console, navigate to **EC2** and click **Launch Instance**.
- Select an Amazon Machine Image (AMI), and choose instance type.
- Configure instance details and subnet as needed.

![Launch Instance](images/ec2-launch.png)

---

### 2. Configure Security Group

- Under **Configure Security Group**, create a new security group or select an existing one.
- Add an **HTTP rule**:
  - Type: HTTP
  - Protocol: TCP
  - Port Range: 80
  - Source: `50.18.32.11/32`

![Security Group HTTP Rule](images/security-group-http.png)

- Add other necessary rules (e.g., SSH for admin access).
- Review and launch the instance.

![Security Group SSH Rule](images/security-group-ssh.png)

---

### 3. Configure Network ACL

- Go to **VPC** > **Network ACLs**.
- Select the NACL associated with your subnet.
- Edit **Inbound Rules**:
  - Rule #: Choose an appropriate number (lowest takes precedence)
  - Type: HTTP
  - Protocol: TCP
  - Port Range: 80
  - Source: `50.18.32.11/32`
  - Allow/Deny: **ALLOW**

![NACL Inbound Rule](images/nacl-inbound.png)

- Edit **Outbound Rules** as required for return traffic:
  - Allow outbound HTTP responses.

![NACL Outbound Rule](images/nacl-outbound.png)

---

### 4. Testing Access

- After configuring the rules, test access from the IP `50.18.32.11` using a browser or `curl`.
- Successful access confirms proper rule setup.

![Access Test](images/access-test.png)

---

### 5. Troubleshooting

- If access is denied:
  - Double-check both Security Group and NACL rules.
  - Ensure no conflicting DENY rules in the NACL.
  - Confirm rule priorities (lowest rule number takes effect for NACL).
  - Check instance health and public IP address.

![Troubleshooting](images/troubleshooting.png)

---

## Best Practices

- Use the principle of least privilege for all security group and NACL rules.
- Regularly audit and review inbound/outbound rules.
- Document all changes for compliance and rollback.
- Pair Security Groups (stateful) with NACLs (stateless) for layered security.

---

## Conclusion

By following this guide, you have learned to:
- Secure AWS EC2 instances with Security Groups and NACLs.
- Allow HTTP access specifically from `50.18.32.11`.
- Troubleshoot and verify connectivity.
- Apply best practices for AWS network security.

This hands-on project strengthens your understanding of cloud security fundamentals and prepares you for advanced AWS networking scenarios.

---
