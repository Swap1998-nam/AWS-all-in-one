# AWS IAM – Identity and Access Management

It solves the problem of **authentication and authorization**.

## Components of IAM
- **Users**
- **Policies**
- **Groups**
- **Roles**

---

## Users
Creation and authentication process will be done here.

---

## Policies
- It specifies **what exact services** are attached to the users.  
- Policies are nothing but **services provided to users to perform some task on services.**

---

## Groups
- A group is a **collection of users with similar access requirements.**  
- Instead of managing permissions for each user individually,  
  we can **directly assign policies or permissions** to groups and then  
  **add users into that group.**

---

## Roles
- IAM roles are **collections of permissions** with **similar access levels.**
- Roles are used to **grant temporary access to AWS resources.**  
- Roles are typically used by **applications or services** that need to access AWS resources on behalf of users or other services.

---

## Tasks in IAM

### User Management
1. Create IAM users  
2. Manage user permissions → assign policies  
3. Change user password / access keys (AWS CLI)  
4. Enable MFA  
5. View user activity → in CloudTrail logs  

### Group Management
1. Create IAM groups → e.g., Dev, Admins, Billing  
2. Attach policies to groups  
3. Add / remove users from groups  

### Role Management
1. Create IAM role → for EC2, Lambda, etc.  
2. Attach policies to the role  

### Policy Management
1. Create custom policies  
2. Attach policies to users or groups  

---

## Monitoring and Auditing
1. Use **CloudTrail logs** → to track *who did what* in AWS  
2. **IAM Credential Reports / AWS account reports**

---

## Important Notes
- **Inline policies** are attached only to **particular users**.  
  (They can’t be attached to others.)
- In IAM, there are two types of managed policies:
  1. **AWS Managed Policies**  
  2. **Customer Managed Policies**

---

## SSM Role (Example)
Whenever **temporary permission** needs to be given to other AWS services, we use a **role**.

**Example:**  
When we have an **EC2 instance in a private subnet** and we want to connect to it,  
we can create an **SSM role (System Manager)**.  
This allows us to **connect without using SSH or jump servers or bastion hosts.**
