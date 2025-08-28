# cloudlaunch-assignment
# CloudLaunch Assignment 🚀

## 📌 Project Overview
This project sets up AWS resources for static website hosting, IAM user access, and a custom VPC design.

The tasks include:
- Hosting a static website in **Amazon S3** (with optional CloudFront distribution).
- Creating IAM policies for secure and limited access.
- Designing a VPC with public, application, and database subnets.
- Configuring security groups to allow proper communication between tiers.

---

## 🌐 S3 Website URLs
- **Static Site Bucket URL:**  
(https://cloudlaunch-site-bucket347.s3.eu-west-1.amazonaws.com/index.html)  

- **CloudFront URL (optional, if created):**  
  https://xxxxxxxxxxxxx.cloudfront.net  

---

## 🔐 IAM Policies

### S3 Access Policy
Allows `cloudlaunch-user` to list and access objects with specific permissions.

File: [`policies/s3-access-policy.json`](policies/s3-access-policy.json)

### VPC Read-Only Policy
Allows read-only (`Describe*`) access to VPC resources.

File: [`policies/vpc-readonly-policy.json`](policies/vpc-readonly-policy.json)

---

## 🌐 VPC Layout

**VPC Name:** `cloudlaunch-vpc`  
**CIDR:** `10.0.0.0/16`

### Subnets
- **Public Subnet:** `10.0.1.0/24` → Internet access via IGW  
- **App Subnet:** `10.0.2.0/24` → Private, no direct internet  
- **DB Subnet:** `10.0.3.0/28` → Private, isolated for databases  

### Internet Gateway
- **Name:** `cloudlaunch-igw`  
- Attached to `cloudlaunch-vpc`

### Route Tables
- **Public Route Table:**  
  - Routes: `10.0.0.0/16 → local`, `0.0.0.0/0 → cloudlaunch-igw`  
  - Associated with: Public Subnet  
- **App Route Table:**  
  - Routes: `10.0.0.0/16 → local`  
  - Associated with: App Subnet  
- **DB Route Table:**  
  - Routes: `10.0.0.0/16 → local`  
  - Associated with: DB Subnet  

### Security Groups
- **cloudlaunch-app-sg:** Allows HTTP (80) from within VPC (`10.0.0.0/16`).  
- **cloudlaunch-db-sg:** Allows MySQL (3306) only from App Subnet (`10.0.2.0/24`).  

---

## 📸 Screenshots (Optional)
- AWS S3 bucket hosting setup  
- VPC and subnet diagram  
- IAM policy console screenshots  

---

## ✅ Deliverables
- Static website hosted on S3  
- IAM policies uploaded in `policies/` folder  
- Documentation (this README)
