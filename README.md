# Three-tier-architecture-with-aws

# Table of Contents

1. [Introduction](#introduction)
   - [Overview of the Project]
   - [Purpose and Goals]
   - [My Role in the Project (AWS Infrastructure Setup)]

2. [Architecture](#architecture)
   - [High-Level Architecture Diagram]
   - [Description of the Three-Tier Setup]
     - [Web Tier]
     - [App Tier]
     - [Database Tier]

3. [Technologies Used](#technologies-used)
   - [AWS Services]
     - [EC2](#ec2)
     - [Elastic Load Balancer (ELB)]
     - [RDS]
     - [S3]

4. [Infrastructure Setup](#infrastructure-setup)
   - [Steps to Set Up]
     - [VPC]
     - [Subnets (Public and Private)]
     - [Security Groups]
     - [Load Balancer]
     - [EC2 Instances]
     - [RDS Database]
   - [Key Configurations]
     - [IAM Roles and Policies]
     - [Auto Scaling (if configured)]

5. [Deployment Process](#deployment-process)
   - [Step-by-Step Guide to Recreate the Setup]
     - [Using AWS Console]
    

6. [Validation](#validation)
   - [Testing Infrastructure]
     - [Verifying Load Balancer Connectivity]
     - [Ensuring EC2 and RDS Communication]

7. [Challenges and Solutions](#challenges-and-solutions)
   - [Key Challenges Faced]
   - [How Issues Were Resolved]
  
8. [Diagrams and Visuals](#diagrams-and-visuals)
   - [Network Diagram]
   - [AWS Management Console Screenshots]
     - [Load Balancer]
     - [EC2 Instances]
     - [RDS Configuration]

9. [Future Enhancements](#future-enhancements)
   - [Potential Improvements to the Current Setup]
   - [Adding More Automation]

10. [Acknowledgments](#acknowledgments)
    - [Reference to Original Repository]
    - [Guidance or Resources You Used]
   

---

### **Introduction**

#### **Overview of the Project**
This project involves the implementation of a **three-tier web architecture** using AWS services, designed to demonstrate a scalable, secure, and efficient deployment framework. The architecture separates the application into three layers: the **Web Tier**, **Application Tier**, and **Database Tier**, ensuring modularity and ease of management. 

The repository, originally inspired by the [AWS Three-Tier Web Architecture Workshop](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop), serves as a template to deploy and understand modern cloud-based application infrastructure. 

Key AWS services utilized include:
- **Elastic Load Balancer (ELB)** for distributing incoming traffic.
- **EC2 Instances** for hosting the application backend.
- **RDS (Relational Database Service)** for managing the database layer.
- **VPC (Virtual Private Cloud)** for isolating the architecture within a secure network.

---

#### **Purpose and Goals**
The primary goal of this project is to showcase the implementation of a **cloud-native three-tier architecture** on AWS. This architecture is designed with the following objectives:
1. **Scalability**: Ensure the system can handle varying levels of traffic through load balancing and auto-scaling.
2. **Security**: Leverage VPCs, subnets, and security groups to protect application components.
3. **High Availability**: Deploy the system across multiple availability zones to minimize downtime.
4. **Modularity**: Maintain a clear separation between tiers for better organization and extensibility.

This project serves as a learning experience to understand AWS services and apply best practices in building and managing cloud infrastructures.

---

#### **My Role in the Project (AWS Infrastructure Setup)**
In this project, I focused on designing and implementing the **AWS infrastructure** to deploy the three-tier architecture. My responsibilities included:

1. **Setting Up the Network:**
   - Configured a **VPC** with public and private subnets across multiple availability zones.
   - Established **route tables** and internet gateways to manage network traffic.

2. **Provisioning Resources:**
   - Deployed **EC2 instances** for the application and backend services.
   - Configured an **RDS instance** for the database tier with appropriate security settings.

3. **Configuring Security:**
   - Created **security groups** to control traffic flow between tiers.
   - Set up IAM roles and policies for secure resource access.

4. **Load Balancer Integration:**
   - Deployed and configured an **Elastic Load Balancer** to distribute traffic across application servers.

5. **Testing and Validation:**
   - Validated connectivity and communication between the tiers.
   - Ensured the architecture was working as intended by simulating traffic and reviewing logs.

This project allowed me to gain hands-on experience with AWS services, particularly focusing on network and infrastructure design, security best practices, and deployment strategies.

---


### **Architecture**

#### **High-Level Architecture Diagram**  
The project follows a **three-tier architecture** deployed on AWS. This architecture separates the application into three layers, each serving a distinct purpose:

1. **Web Tier**: Handles incoming user requests.
2. **Application Tier**: Processes business logic.
3. **Database Tier**: Stores persistent data.

![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/three%20tier%20diagram.png)

#### **Description of the Three-Tier Setup**  

1. **Web Tier**:  
   - The **Elastic Load Balancer (ELB)** serves as the entry point, distributing incoming traffic to the application servers.  
   - It ensures fault tolerance and high availability by routing traffic to healthy instances across multiple availability zones.

2. **App Tier**:  
   - The **EC2 instances** in private subnets host the application logic.  
   - These instances are configured with security group rules to allow traffic only from the ELB and communicate with the database tier.  
   - Auto Scaling is used to handle varying loads by dynamically increasing or decreasing the number of instances.

3. **Database Tier**:  
   - The **RDS instance** hosts the database, providing a secure and reliable way to store application data.  
   - RDS is deployed in private subnets to ensure that it is not accessible directly from the internet.  
   - Backups and multi-AZ replication are configured to enhance reliability.

---

### **Technologies Used**

#### **AWS Services**
1. **EC2 (Elastic Compute Cloud)**:  
   - Hosts the application in the App Tier.
   - Configured for scalability and secured with security groups.

2. **Elastic Load Balancer (ELB)**:  
   - Distributes traffic among the EC2 instances in the Web Tier.
   - Enhances fault tolerance and load balancing.

3. **RDS (Relational Database Service)**:  
   - Manages the database in the Database Tier.
   - Provides automated backups, monitoring, and multi-AZ deployment.

4. **S3 **:  
   *For storing static assets like configuration files and application code.


---

### **Infrastructure Setup**

#### **Steps to Set Up**  

1. **VPC**:  
   - Create a **Virtual Private Cloud (VPC)** with a custom CIDR block (e.g., `10.0.0.0/16`) to isolate the network.  
   - Enable **DNS hostnames** to allow instances to communicate using domain names.

2. **Subnets (Public and Private)**:  
   - **Public Subnets**:  
     - Create subnets in different availability zones for high availability.  
     - Associate the subnets with an **internet gateway** for external access.  
   - **Private Subnets**:  
     - Configure subnets for application and database tiers without direct internet access.  
     - Use **NAT gateways** in public subnets for outgoing traffic.

3. **Security Groups**:  
   - **Web Tier (Load Balancer Security Group)**:  
     - Allow inbound HTTP/HTTPS traffic from `0.0.0.0/0`.  
     - Allow inbound health check requests from the App Tier security group.  
   - **App Tier (EC2 Security Group)**:  
     - Allow traffic only from the Load Balancer Security Group on application ports (e.g., `8080`).  
     - Allow outbound traffic to the Database Tier security group.  
   - **Database Tier (RDS Security Group)**:  
     - Allow inbound traffic only from the App Tier security group on port `3306` (MySQL) or relevant DB port.

4. **Load Balancer**:  
   - Deploy an **Application Load Balancer (ALB)** in the Web Tier.  
   - Configure **target groups** with health checks for the EC2 instances.  
   - Attach the ALB to public subnets for external accessibility.

5. **EC2 Instances**:  
   - Launch EC2 instances in private subnets for the application tier.  
   - Use an **Amazon Linux 2** AMI and configure the required software.  
   - Assign IAM roles for access to resources like S3 or CloudWatch (if applicable).

6. **RDS Database**:  
   - Deploy an **RDS instance** in private subnets.  
   - Choose the database engine (e.g., MySQL, PostgreSQL) and configure multi-AZ deployment.  
   - Set up automated backups and enable monitoring for performance insights.

---

#### **Key Configurations**  

1. **IAM Roles and Policies**:  
   - Create an IAM role for the EC2 instances with permissions to:  
     - Access S3 buckets.  
     - Push logs to CloudWatch for monitoring and debugging.  
   - Restrict permissions to follow the **least privilege principle**.

2. **Auto Scaling**:  
   - Configure an **Auto Scaling Group (ASG)** for the App Tier EC2 instances.  
   - Define scaling policies based on metrics like CPU utilization or network traffic.  
   - Set a minimum and maximum number of instances to maintain cost efficiency while handling traffic spikes.

---

### **Deployment Process**

#### **Step-by-Step Guide to Recreate the Setup Using AWS Console**

1. **Set Up the VPC**:  
   - Go to the **VPC** service in the AWS Management Console.  
   - Click **Create VPC** and configure:  
     - Name: `Three-Tier-VPC`  
     - CIDR Block: `10.0.0.0/16`  
   - Enable DNS resolution and hostnames.

2. **Create Subnets**:  
   - Create **Public Subnets**:  
     - Assign CIDR blocks like `10.0.1.0/24` and `10.0.2.0/24`.  
     - Select different availability zones (e.g., `us-east-1a`, `us-east-1b`).  
   - Create **Private Subnets**:  
     - Assign CIDR blocks like `10.0.3.0/24` and `10.0.4.0/24`.  
     - Use separate availability zones.

3. **Set Up the Internet Gateway**:  
   - Attach an **Internet Gateway** to the VPC.  
   - Update the route table for public subnets to allow internet traffic.

4. **Set Up Security Groups**:  
   - **Web Tier Security Group**:  
     - Allow inbound HTTP (port 80) and HTTPS (port 443) traffic from `0.0.0.0/0`.  
     - Allow outbound traffic to all destinations.  
   - **App Tier Security Group**:  
     - Allow inbound traffic from the Web Tier Security Group.  
     - Allow outbound traffic to the Database Tier Security Group.  
   - **Database Tier Security Group**:  
     - Allow inbound traffic from the App Tier Security Group on port `3306` (MySQL).  
     - Restrict outbound traffic to necessary destinations only.

5. **Deploy the Load Balancer (Web Tier)**:  
   - Navigate to the **EC2 > Load Balancers** section.  
   - Create an **Application Load Balancer** and:  
     - Assign it to public subnets.  
     - Create a **Target Group** for App Tier EC2 instances.  
     - Configure health checks.

6. **Launch EC2 Instances (App Tier)**:  
   - Navigate to **EC2 > Instances** and click **Launch Instance**.  
   - Select an **Amazon Linux 2 AMI** and appropriate instance type.  
   - Attach the App Tier Security Group.  
   - Assign the EC2 instances to private subnets.  
   - Install and configure the application using user data or manual SSH commands.

7. **Set Up the RDS Database (Database Tier)**:  
   - Go to the **RDS** service and click **Create Database**.  
   - Choose the database engine (e.g., MySQL), version, and instance type.  
   - Assign the Database Tier Security Group.  
   - Configure the database to be in private subnets and enable multi-AZ replication.

8. **Configure IAM Roles and Policies**:  
   - Create an IAM role for EC2 instances to grant permissions for accessing resources like S3 or CloudWatch.  
   - Attach the role to the App Tier EC2 instances.

9. **Enable Auto Scaling (Optional)**:  
   - Navigate to **Auto Scaling Groups** under the EC2 dashboard.  
   - Configure a scaling policy based on CPU utilization or other metrics.  
   - Attach the scaling group to the App Tier EC2 instances.

10. **Test and Validate**:  
    - Verify that the load balancer is correctly distributing traffic.  
    - Check the connectivity between the EC2 instances and the RDS database.  
    - Ensure security group rules are correctly configured.

---

### **Validation**

### **Testing Infrastructure**

#### **Verifying Load Balancer Connectivity**  
1. Access the Load Balancer’s DNS name from the AWS Management Console.  
2. Open the DNS name in a browser to ensure it routes traffic to the application.  
   - If the application is not accessible, check the security group rules for the Load Balancer.  
   - Verify health checks for target instances in the Load Balancer configuration.

#### **Ensuring EC2 and RDS Communication**  
1. SSH into an EC2 instance in the App Tier.  
2. Test database connectivity using the following command (replace placeholders):  
   ```bash
   mysql -h <RDS_ENDPOINT> -u <DB_USER> -p
   ```  
3. Ensure the database is reachable by running simple SQL queries.  
   - If connectivity fails, verify:  
     - Security Group rules for the RDS instance.  
     - Network ACLs for the private subnets.


---

### **Challenges and Solutions**

#### **Key Challenges Faced**  
1. **Load Balancer Health Check Failures**:  
   - Instances failed health checks due to incorrect application port settings.  
2. **Database Connectivity Issues**:  
   - Misconfigured security group rules blocked traffic between the App Tier and the Database Tier.  
3. **Scaling Configurations**:  
   - Auto Scaling policies were not triggering as expected due to incorrect metric thresholds.

#### **How Issues Were Resolved**  
1. **Health Check Failures**:  
   - Verified application configurations to ensure it was listening on the correct port.  
   - Updated the Load Balancer health check target.  
2. **Database Connectivity Issues**:  
   - Reviewed and updated RDS security group rules to allow inbound traffic from App Tier instances.  
3. **Scaling Configurations**:  
   - Adjusted scaling policies by monitoring CloudWatch metrics and fine-tuning thresholds.

---

### **Diagrams and Visuals**

#### **Network Diagram**  
- Provide a visual representation of the architecture, including:  
  - VPC with public and private subnets.  
  - Load Balancer, EC2 instances, and RDS placement.  
 
#### **AWS Management Console Screenshots**  
**Load Balancer**:

![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/lb.png)
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/apptier-lb.png)
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/webtier-lb.png)

**EC2 Instances**:  

![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/app%20ec2.png)
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/web%20ec2.png)

**RDS Configuration**:  
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/rds.png)
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/cbe44125ff3f7e895c6430d7494d97e0c09f5b4e/application-code/project%20ss/db%20subnet%20group.png)


**Final Working**:
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/079c062b171894a98ba0785a43764dca3de03323/application-code/project%20ss/final%20ss%201.png)
![alt text](https://github.com/mehraakshat-ops/Three-tier-architecture-with-aws/blob/079c062b171894a98ba0785a43764dca3de03323/application-code/project%20ss/final%20ss%202.png)

---

### **Future Enhancements**

#### **Potential Improvements to the Current Setup**  
1. **Adding More Automation**:  
   - Use **Terraform** or **AWS CloudFormation** to automate the entire infrastructure setup.  
2. **Improved Monitoring**:  
   - Configure **CloudWatch Alarms** for more detailed monitoring and notifications.  
3. **Increased Fault Tolerance**:  
   - Implement multi-region deployment for disaster recovery.

---

### **Acknowledgments**

- Reference to the original repository:  
  [AWS Three-Tier Web Architecture Workshop](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop.git)  
- Special thanks to the resources and guides used during the project implementation.

---

- **Guidance or Resources Used**:  
  - Official AWS Documentation for EC2, RDS, and Load Balancer setup.  
  - AWS Well-Architected Framework for designing a scalable and fault-tolerant infrastructure.  
  - Community tutorials and forums for troubleshooting and optimizing configurations.  

---
