# Identity and Access Management (IAM)

## 1. What Is IAM?

Identity and Access Management (IAM) is the collection of processes, policies, and technologies used to manage digital identities and control access to systems and resources.

The central questions are:

```text
Who are you?
What are you allowed to access?
What are you allowed to do?
How is that access managed and reviewed?
```

IAM is especially important when users, applications, devices, and services access resources from many different locations.

---

# 2. Identity as a Security Perimeter

Traditional security often focused heavily on protecting a network perimeter.

Modern environments have users and resources distributed across:

- Corporate networks
- Remote networks
- Cloud platforms
- SaaS applications
- Mobile devices
- External services

Because of this, knowing and verifying the identity of the requester becomes a major security control.

```text
Request
   ↓
Identify requester
   ↓
Verify identity
   ↓
Evaluate permissions
   ↓
Allow or deny access
```

---

# 3. The Four As of IAM

A useful way to organize IAM is through four major functions:

```text
Administration
Authentication
Authorization
Audit
```

## Administration

Manages identities and their access throughout their lifecycle.

## Authentication

Determines who a user or entity is.

## Authorization

Determines whether the entity is permitted to perform a requested action.

## Audit

Records and reviews identity and access activity.

---

# 4. User Groups

An IAM architecture should understand the different groups of users that need access.

Examples include:

```text
Employees
Suppliers
Customers
Partners
Administrators
Contractors
```

An employee population may be divided further:

```text
Employees
├── Administration
├── Manufacturing
└── Sales
```

Customers can also have different groups:

```text
Customers
├── Commercial
└── Retail
```

The purpose is to understand what each group needs to access.

---

# 5. User Capabilities

Different users require different capabilities.

Examples of enterprise resources include:

```text
HR System
Email
CRM
Finance System
File Storage
Business Applications
```

Example:

```text
Sales Employee
├── Email   → Yes
├── CRM     → Yes
├── HR      → Yes
└── Finance → No
```

IAM connects the user identity to the permissions required by that user's responsibilities.

---

# 6. Identity Directories

A directory stores identity information that applications and security systems can use.

Typical information may include:

```text
Name
Account
Department
Role
Group
Attributes
```

A directory provides a central or coordinated location for identity-related information.

---

# 7. Multiple Directories

Large organizations may not have every identity stored in one directory.

Different systems can maintain their own identity stores.

```text
Directory A
     |
Directory B
     |
Directory C
```

IAM architecture therefore needs ways to connect and synchronize identity information.

---

# 8. Directory Synchronization

## Virtual Directory

A virtual directory acts as an index or abstraction layer.

```text
                 Virtual Directory
                  /      |      \
                 /       |       \
          Directory A Directory B Directory C
```

When information is requested, the virtual directory can locate the appropriate underlying directory.

A cache can be used in some architectures to improve performance.

### Main idea

The information may remain in the original directories while the virtual layer provides a unified way to find it.

## Meta Directory

A meta directory copies selected identity information from multiple sources into a higher-level enterprise directory.

```text
Directory A ──┐
Directory B ──┼──→ Enterprise Directory
Directory C ──┘
```

Only relevant information may need to be synchronized.

### Main idea

The enterprise directory already contains the required information when an application needs it.

---

# 9. Administration

Administration covers the management of identity and access throughout its lifecycle.

Typical tasks include:

```text
Create account
     ↓
Update account
     ↓
Change role
     ↓
Change privileges
     ↓
Remove account
```

This area is often associated with:

- Identity management
- Identity governance
- Account administration
- Role management

---

# 10. Provisioning

Provisioning is the process of creating and assigning accounts and access for a user.

```text
Employee joins organization
        ↓
User identity created
        ↓
Role assigned
        ↓
Required accounts created
        ↓
Required permissions granted
```

A good provisioning process provides only the access required by the user's responsibilities.

---

# 11. De-Provisioning

When a person leaves an organization or no longer needs access, their access should be removed.

```text
Employee leaves
       ↓
Account disabled
       ↓
Access removed
       ↓
Sessions/tokens handled
       ↓
Resources reassigned
```

Failure to remove unnecessary access can leave unused accounts as security risks.

---

# 12. Role Management

Users can be mapped to roles based on their business responsibilities.

```text
Business Role
      ↓
IT Role
      ↓
Required Access
```

Example:

```text
Sales Employee
      ↓
Sales Role
      ↓
CRM + Email + Sales Tools
```

Role-based access simplifies management at scale because users can receive permissions through roles instead of individual assignments.

---

# 13. Authentication

Authentication answers:

> Who are you?

Traditional authentication factors are commonly grouped into three categories.

## Something You Know

Examples:

```text
Password
PIN
Passphrase
```

Knowledge can be copied, disclosed, guessed, or stolen.

## Something You Have

Examples:

```text
Mobile phone
Security token
Hardware security key
Authenticator device
```

The user proves possession of a physical device or credential.

## Something You Are

This refers to a biometric characteristic.

Examples:

```text
Fingerprint
Face
Other biometric characteristic
```

The system uses a measurable physical characteristic to help verify identity.

---

# 14. Multi-Factor Authentication

Multi-Factor Authentication (MFA) uses multiple independent authentication factors.

```text
Something You Know
        +
Something You Have
        =
MFA
```

Example:

```text
Password
   +
Mobile authentication
   +
Biometric verification
```

MFA reduces the risk associated with a compromised password because possession of the password alone is not sufficient.

---

# 15. Single Sign-On

Single Sign-On (SSO) allows a user to authenticate once and then access multiple authorized applications without separately logging into each one.

Without SSO:

```text
Application A → Login
Application B → Login
Application C → Login
Application D → Login
```

With SSO:

```text
             Identity Provider
                    ↓
                  Login
                    ↓
       ┌────────────┼────────────┐
       ↓            ↓            ↓
     App A        App B        App C
```

MFA can be combined with SSO to strengthen the initial authentication event.

---

# 16. Authorization

Authorization answers:

> What are you allowed to do?

Basic model:

```text
Authenticated User
        ↓
Requested Action
        ↓
Authorization Decision
       / \
    Allow Deny
```

Authentication does not automatically mean that every requested action is allowed.

---

# 17. Risk-Based Authorization

Authorization can consider context instead of applying only a simple allow/deny rule.

Possible factors include:

```text
User identity
Location
Device
Request type
Transaction amount
Frequency
Risk level
```

Example:

```text
Normal login
    ↓
Low risk
    ↓
Allow
```

A high-value or unusual transaction may require additional controls.

---

# 18. Adaptive Access

Adaptive access can change security requirements depending on circumstances.

```text
Normal activity
      ↓
Low risk
      ↓
Standard authentication
```

But:

```text
Unusual location
      +
Unusual device
      +
Sensitive operation
      ↓
Higher risk
      ↓
Additional verification
```

The basic idea is to apply stronger controls when the situation appears riskier.

---

# 19. Transaction Context

Not every activity has the same risk.

For example:

```text
View account information
        ↓
Lower-risk action
```

compared with:

```text
Transfer money
        ↓
Higher-risk action
```

Authorization systems can use the type of requested action when deciding what controls to apply.

---

# 20. Transaction Amount

The amount involved in an action can influence risk.

```text
Small transaction
      ↓
Normal controls
```

```text
Large transaction
      ↓
Stronger controls
```

Organizations can create thresholds that trigger additional verification or approval.

---

# 21. Frequency Analysis

Unusual activity frequency can be a useful risk signal.

```text
Normal behavior:
1 transaction per month

Observed behavior:
30 transactions in one day
```

A large change from a normal pattern may justify additional verification or investigation.

---

# 22. Privileged Access Management

Privileged Access Management (PAM) focuses on highly privileged accounts.

Examples:

```text
Root account
System administrator
Database administrator
Network administrator
Cloud administrator
```

These accounts can make changes that affect large portions of an environment.

They may be able to:

```text
Change configurations
Access sensitive data
Create accounts
Modify security settings
Change network controls
Delete or alter resources
```

---

# 23. Why Privileged Accounts Need Extra Protection

A compromised ordinary account may expose a limited set of resources.

A compromised privileged account may provide much broader access.

```text
Normal Account
     ↓
Limited Resources
```

versus:

```text
Privileged Account
     ↓
Many Critical Resources
```

Useful safeguards include:

- Strong authentication
- MFA
- Restricted administrative access
- Monitoring
- Logging
- Controlled privilege elevation
- Separate administrative identities

---

# 24. Workforce Identity Management

Workforce IAM focuses on people who work for or operate within an organization.

Examples:

```text
Employees
Contractors
Administrators
Partners
Suppliers
```

Typical requirements include:

- Employee onboarding
- Role assignment
- Provisioning
- Privilege changes
- Access reviews
- Offboarding
- Administrative account protection

---

# 25. Consumer Identity Management

Consumer IAM focuses on external customers or users of a service.

```text
Customer
   ↓
Create Account
   ↓
Authenticate
   ↓
Access Customer Services
```

Common requirements include:

- Easy account creation
- Authentication
- User experience
- Password recovery
- MFA
- Privacy
- Scalable identity services

Consumer IAM can have different priorities from internal workforce IAM.

---

# 26. IAM Lifecycle

A complete identity lifecycle can be represented as:

```text
Identify Need
     ↓
Create Identity
     ↓
Assign Role
     ↓
Provision Access
     ↓
Authenticate
     ↓
Authorize
     ↓
Monitor
     ↓
Review
     ↓
Modify Access
     ↓
De-Provision
```

The lifecycle should continue as responsibilities change.

---

# 27. Auditing

Audit is the fourth "A" in IAM.

Auditing involves recording and reviewing identity and access activity.

Examples:

```text
Login
Logout
Access request
Permission change
Role change
Account creation
Account deletion
Privileged activity
```

Simplified flow:

```text
User Activity
      ↓
Event Recorded
      ↓
Log Storage
      ↓
Review / Analysis
      ↓
Investigation if Required
```

Auditing provides visibility into activity and supports investigations and accountability.

---

# 28. IAM Architecture

A simplified IAM architecture may look like:

```text
                    Users
             /        |        \
        Employees   Customers   Suppliers
             \        |        /
                    Identity
                       |
              -------------------
              |                 |
         Directory          Administration
              |                 |
       Synchronization      Role Management
              |
         Authentication
              |
             MFA
              |
         Authorization
              |
       Risk / Context
              |
          Applications
              |
         Audit / Logs
```

The architecture connects identity data, authentication, authorization, administration, and auditing.

---

# 29. Core IAM Questions

Every IAM architecture should be able to answer:

```text
Who is this user?

How was the identity verified?

What role does the user have?

What resources should the user access?

What actions may the user perform?

How is the access provisioned?

How is access changed?

How is access removed?

How is activity recorded?

How are privileged accounts protected?
```

---

# 30. Key Terms

| Term | Meaning |
|---|---|
| IAM | Identity and Access Management |
| Authentication | Establishing who an entity is |
| Authorization | Determining what an entity can do |
| Administration | Managing identities and access |
| Audit | Recording and reviewing access activity |
| Directory | Store of identity-related information |
| Virtual Directory | Unified interface/index over multiple directories |
| Meta Directory | Enterprise directory containing synchronized identity information |
| Provisioning | Creating accounts and granting required access |
| De-provisioning | Removing or disabling access |
| RBAC | Role-Based Access Control |
| MFA | Multi-Factor Authentication |
| SSO | Single Sign-On |
| PAM | Privileged Access Management |
| Adaptive Access | Adjusting access controls based on context and risk |

---

# 31. Final Mental Model

```text
                    IAM
                     |
       ---------------------------------------
       |          |          |               |
Administration Authentication Authorization Audit
       |          |          |               |
   Accounts      Who?       What?        What happened?
   Roles         MFA        Risk         Logs
   Provision     SSO        Context      Reviews
   Removal
```

The overall objective is to ensure that the right identity receives the right access, under the right conditions, for the right amount of time, while activity remains visible and reviewable.
