# Active Directory Lab on AWS

## Overview
Personal lab project simulating enterprise identity and access management using Windows Server Active Directory hosted on AWS EC2.

## Environment
- Windows Server 2022 running on an AWS EC2 instance
- Promoted to a Domain Controller hosting a new Active Directory forest (mylab.local)
- Second EC2 instance (Client01) joined to the domain as a member server
- AWS account access managed through IAM; RDP restricted to a single IP via security group

## What I Did
- Deployed and configured a Windows Server instance on AWS EC2
- Installed Active Directory Domain Services and promoted the server to a Domain Controller
- Created organizational units (OUs) for IT, HR, and Sales
- Created user accounts and placed them in their departments
- Created a security group (IT-Admins) and added a user to demonstrate group-based access management
- Configured a Group Policy enforcing a 12-character minimum password length
- Verified the password policy and user accounts in PowerShell (Get-ADDefaultDomainPasswordPolicy, Get-ADUser)
- Deployed a second EC2 instance (Client01), set its DNS to the domain controller, and joined it to mylab.local
- Logged into Client01 as a domain user to confirm centralized authentication

## Troubleshooting
- After DC promotion, local admin login failed; resolved by signing in with the domain account (MYLAB\Administrator)
- Screenshot shortcuts were intercepted by the RDP session; used the Snipping Tool app instead
- File transfer from the server failed with clipboard and drive redirection disabled; uploaded directly to GitHub from the server
- Client01 could not resolve mylab.local because it was using the AWS default DNS; set its DNS server to the domain controller's private IP and confirmed with nslookup
- Domain join failed using the user's display name; AD authenticates on the pre-Windows 2000 logon name found under the Account tab
- Domain join returned "the specified network name is no longer available" due to a typo in the domain name
- Domain user was denied RDP access to Client01; resolved by adding the account to the local Remote Desktop Users group

## Screenshots
**OU structure with user and security group**
![OU structure](01-ou-structure.PNG)

**IT-Admins group membership**
![Group membership](02-group-membership.PNG)

**Password policy set to 12 characters**
![Password policy](03-password-policy.PNG)

**PowerShell verification of policy and users**
![Powershell verification](04-powershell-verification.PNG)

**Client DNS pointed to DC**
![Client dns config](05-client-dns-config.PNG)

**Client01 joined to domain**
![Domain join](06-domain-join.PNG)

**Domain user login as jsmith**
![Domain user login](07-domain-user-login.PNG)
