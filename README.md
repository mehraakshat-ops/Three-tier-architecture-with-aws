# Three-tier-architecture-with-aws

# Table of Contents

1. [Introduction](#introduction)
   - [Overview of the Project](#overview-of-the-project)
   - [Purpose and Goals](#purpose-and-goals)

2. [Architecture](#architecture)
   - [High-Level Architecture Diagram](#high-level-architecture-diagram)
   - [Description of the Three-Tier Setup](#description-of-the-three-tier-setup)
     - [Web Tier](#web-tier)
     - [App Tier](#app-tier)
     - [Database Tier](#database-tier)

3. [Technologies Used](#technologies-used)
   - [AWS Services](#aws-services)
     - [EC2](#ec2)
     - [Elastic Load Balancer (ELB)](#elastic-load-balancer-elb)
     - [RDS](#rds)
     - [S3](#s3)

4. [Infrastructure Setup](#infrastructure-setup)
   - [Steps to Set Up](#steps-to-set-up)
     - [VPC](#vpc)
     - [Subnets (Public and Private)](#subnets-public-and-private)
     - [Security Groups](#security-groups)
     - [Load Balancer](#load-balancer)
     - [EC2 Instances](#ec2-instances)
     - [RDS Database](#rds-database)
   - [Key Configurations](#key-configurations)
     - [IAM Roles and Policies](#iam-roles-and-policies)
     - [Auto Scaling (if configured)](#auto-scaling-if-configured)

5. [Deployment Process](#deployment-process)
   - [Step-by-Step Guide to Recreate the Setup](#step-by-step-guide-to-recreate-the-setup)
     - [Using AWS Console](#using-aws-console)
    

6. [Validation](#validation)
   - [Testing Infrastructure](#testing-infrastructure)
     - [Verifying Load Balancer Connectivity](#verifying-load-balancer-connectivity)
     - [Ensuring EC2 and RDS Communication](#ensuring-ec2-and-rds-communication)

7. [Challenges and Solutions](#challenges-and-solutions)
   - [Key Challenges Faced](#key-challenges-faced)
   - [How Issues Were Resolved](#how-issues-were-resolved)

8. [Diagrams and Visuals](#diagrams-and-visuals)
   - [Network Diagram](#network-diagram)
   - [AWS Management Console Screenshots](#aws-management-console-screenshots)
     - [Load Balancer](#load-balancer)
     - [EC2 Instances](#ec2-instances)
     - [RDS Configuration](#rds-configuration)

9. [Future Enhancements](#future-enhancements)
   - [Potential Improvements to the Current Setup](#potential-improvements-to-the-current-setup)
   - [Adding More Automation](#adding-more-automation)

10. [Acknowledgments](#acknowledgments)
    - [Reference to Original Repository](#reference-to-original-repository)
    - [Guidance or Resources You Used](#guidance-or-resources-you-used)
