# AWS Three-Tier Web Architecture Workshop

## Overview
This project offers a practical experience in building a three-tier web architecture on AWS. Participants will manually set up the required network, security, application, and database components to ensure the architecture is both available and scalable.

## Architecture Summary
![Image](https://github.com/user-attachments/assets/bbb5b9b5-b5a0-47ca-bee8-bd2765e259b7)
This design utilizes a public-facing Application Load Balancer to direct client traffic to EC2 instances in the web tier. These instances run Nginx servers configured to host a React.js website and forward API requests to an internal load balancer in the application tier. The internal load balancer then routes the requests to Node.js-based application servers. These servers interact with an Aurora MySQL multi-AZ database to process and return data to the web tier. Load balancing, health checks, and auto-scaling groups are implemented across each layer to ensure continuous availability.

## Implementation Steps
### AWS Project: Building a Three-Tier Architecture & Integrating Additional AWS Services

### Step 1: Clone the Repository from GitHub
Download the project repository to your local machine.

### Step 2: Set Up Two S3 Buckets
- **One bucket for storing the web and app server code**.
  - Upload the code from your local environment.
- **Another bucket for storing VPC flow logs**.

### Step 3: Create an IAM Role with Specific Policies
- Grant **S3 read-only** access.
- Include the **SSM managed instance core** policy.

### Step 4: Set Up VPC, Subnets, IGW, NAT Gateway, and Route Tables
- Enable auto-assignment of public IPs for the web-tier public subnets.
- Configure flow logs for the VPC, storing them in the designated S3 bucket.

### Step 5: Define Security Groups
- `External-Load-Balancer-SG`: Allow **HTTP (80)** from any IP (`0.0.0.0/0`).
- `Web-Tier-SG`: Allow **HTTP** from `External-Load-Balancer-SG`.
- `Internal-Load-Balancer-SG`: Allow **HTTP** from `Web-Tier-SG`.
- `App-Tier-SG`: Allow **port 4000** from `Internal-Load-Balancer-SG`.
- `DB-Tier-SG`: Allow **MySQL (3306)** from `App-Tier-SG`.

### Step 6: Configure DB Subnet Group & RDS Instance
- Create a **database subnet group**.
- Deploy a **multi-AZ RDS instance** within this subnet group.

### Step 7: Set Up and Test the Application Server
- Run initial commands on the app server.
- Create an **AMI**, then use it for a launch template.
- Set up a **target group** and **internal load balancer**.
- Modify `nginx.conf` locally, then upload the updated file to S3.

### Step 8: Set Up and Test the Web Server
- Install necessary packages (**Nginx, Node.js** for React).
- Run initial commands on the web server.
- Create an **AMI**, then use it for a launch template.
- Set up a **target group** and **external load balancer**.

### Step 9: Add DNS Record for External ALB in Route 53

### Step 10: Configure CloudWatch Alarms and SNS Notifications

### Step 11: Enable CloudTrail

### Step 12: Tear Down the Infrastructure
- Sequentially delete **CloudFront distributions**, **CloudWatch alarms**, **Route 53 records**, **load balancers**, **target groups**, **auto-scaling groups**, **launch templates**, **security groups**, **NAT gateways**, **elastic IPs**, **VPCs**, **RDS subnet groups**, and **RDS instances**.

## Instructions for the Workshop
For detailed guidance, see [AWS Three-Tier Web Architecture](#).
