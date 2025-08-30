# AWS IAM Project Documentation

## ***Implementing Identity & Access Management with Security Best Practices (Cloud/DevOps Engineering)***

## **Overview:**

In this project, I implemented secure Identity and Access Management (IAM) in AWS—a core skill for any Cloud or DevOps Engineer. The goal was to:

- Establish a **secure, role-based access control system**.
- Enforce **Multi-Factor Authentication (MFA)**.
- Implement **group-level permission management** using **AWS security best practices**.
- Set up **IAM roles** for services (e.g., EC2), enhancing **least privilege principles**.

✅

**Security Focus:**

From the beginning, this project prioritizes strong access governance, credential protection, and scalable permission assignment—all essential to reduce attack surface in any cloud-native organization

## **Project Objectives:**

- Secure the AWS root account with MFA.
- Create IAM users with unique credentials and MFA enforcement.
- Structure teams into IAM groups with defined permission sets.
- Assign permission policies at **group level** (not individual), in line with AWS best practices.
- Create IAM roles for EC2 to enable secure service communication.
- Emphasize principles like **least privilege**, **separation of duties**, and **auditable identity actions**.

## **1. Securing the Root Account:**

### The first and most critical step was **securing the root account**.

Using the **IAM dashboard**, I:

- Enabled **MFA for root user** via a virtual authenticator app (e.g., Google Authenticator).
- Stored root credentials offline and avoided daily login with root.

![IAM 1.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_1.png)

### **Best Practice:** Root account should only be used for initial account setup and essential billing/config tasks. MFA is mandatory for this high-privilege identity.

## **🔗 2. Creating an Account Alias:**

To enhance usability and avoid AWS’s default long login URLs, I:

- Created a custom **account alias** (e.g., company-alias) to generate a user-friendly login endpoint.

📎 *Screenshot Placeholder: Creating Account Alias*

![IAM 2.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_2.png)

### 🧠 **Insight:** This improves user experience and ensures users are always directed to the correct AWS organization console.

## **3. IAM Users: Creation, Login & MFA Activation:**

Using the IAM console, I:

- Created multiple IAM users with **console access**.
- Downloaded their initial credentials.
- Shared login URLs for secure user-specific access.

Each user was then:

- Logged into the AWS Console via the **IAM sign-in link**.
- Prompted to reset the password.
- Assigned a **MFA virtual device** and activated it.

![IAM 3.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_3.png)

![IAM 4.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_4.png)

![IAM 5.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_5.png)

![IAM 6.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_6.png)

![IAM 7.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_7.png)

![IAM 8.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_8.png)

### ✅ **Best Practice:** Every IAM user should use **MFA** and **password policies** must enforce complexity and rotation. This secures against stolen credential misuse.

## **4. Creating IAM Groups Based on Team Roles:**

Instead of assigning permissions directly to users (which is **bad practice**), I created three groups:

| **Group Name** | **Purpose** |
| --- | --- |
| Admin Team | Full administrative control |
| DevOps Team | Infrastructure and deployment permissions |
| Developer Team | Limited access for coding and testing |

![IAM 9.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_9.png)

![IAM 10.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_10.png)

![IAM 11.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_11.png)

### Users were added to their respective groups.

### 📌 **Security Principle: Least Privilege**

### Always grant **only the permissions needed** for each role. This minimizes risk from insider threats or user error.

## **5. Group-Level Permission Assignment:**

### Using the IAM policy library, I attached permissions to **groups**, not individual users:

| **Group Name** | **Assigned Policy** |
| --- | --- |
| Admin Team | AdministratorAccess |
| DevOps Team | PowerUserAccess, SystemAdmin (custom) |
| Developer Team | DataScientist (custom policy) |

   

![IAM 12.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_12.png)

### 

![IAM 13.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_13.png)

![IAM 14.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_14.png)

### ✅ **Why Group-Based Access is Better:**

### It ensures **consistency**, **easier audits**, and **simplifies revocation** when users change roles or leave the organization

## 6.  **IAM Role Creation for EC2 (Service Roles):**

IAM roles allow services like **EC2** to securely access other AWS services **without using long-term credentials**.

Steps taken:

- Selected **"AWS Service"** as the trusted entity.
- Chose **EC2**.
- Created a role: EC2-ROLE-01.
- Attached AmazonS3FullAccess and CloudWatchFullAccess.
- 

![IAM 15.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_15.png)

![IAM 16.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_16.png)

![IAM 17.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_17.png)

### 💡 **Security Insight:**

### IAM roles use **temporary credentials** provided by the **AWS Security Token Service (STS)**, reducing the risk of key leaks

## **7. Testing Access & Verifying Setup:**

To confirm configurations:

- Logged in with each IAM user to ensure appropriate access.
- Verified permission boundaries (e.g., Developer Team cannot access administrative settings).
- Validated MFA prompt at every login.

Used custom sign-in alias to streamline login experience

### 

![IAM 18.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_18.png)

![IAM 19.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_19.png)

![IAM 20.png](AWS%20IAM%20Project%20Documentation%201975c4233bb6805eade3c6f79590ef1f/IAM_20.png)

## **🧠 Security Best Practices Followed**

| **Practice** | **Benefit** |
| --- | --- |
| Enabling MFA on all accounts | Prevents unauthorized access |
| Never using root for daily tasks | Minimizes risk from high-privilege misuse |
| Group-based permission assignment | Easier auditing, onboarding/offboarding users |
| Role-based service access | Avoids hardcoded credentials and improves security |
| Unique IAM user per person | Enables individual audit trails and traceability |
| Short login alias URLs | Prevents phishing and increases user confidence |

## **Lessons Learned**
• IAM is at the **core of cloud security**. Misconfigurations can lead to serious data breaches.

> 
> 
> 
> © 2025 Iniabasi Okorie | All Rights Reserved
> 
> 🔗 LinkedIn: [linkedin.com/in/iniabasiokorie](https://linkedin.com/in/iniabasiokorie)
> 
> 📌 Please do not copy, reproduce, or republish this content without permission.
>