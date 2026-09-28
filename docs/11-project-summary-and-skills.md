# 11 - Project Summary and Skills Demonstrated

## 11.1 Project Overview

The CyberShield Active Directory Lab was built to develop and demonstrate practical Windows Server, Active Directory, networking, security, troubleshooting, and IT support skills in a realistic virtual environment.

The lab was created using Microsoft Hyper-V with Windows Server 2022 and Windows 11 Pro.

Rather than only installing Active Directory, the project was developed into a small enterprise-style environment containing organisational units, users, security groups, Group Policy, departmental file shares, access controls, account security policies, troubleshooting scenarios, backup and recovery, and network documentation.

---

## 11.2 Environment

| Component | Configuration |
|---|---|
| Hypervisor | Microsoft Hyper-V |
| Hyper-V Host | `JAHIDUL-LAPTOP` |
| Host OS | Windows 11 Pro |
| Domain Controller | `DC01` |
| Server OS | Windows Server 2022 |
| Client Workstation | `CLIENT01` |
| Client OS | Windows 11 Pro |
| Active Directory Domain | `cybershield.test` |
| Domain Controller / DNS | `10.50.0.10` |
| Client IP | `10.50.0.20` |
| Lab Network | `10.50.0.0/24` |
| Virtual Switch | `CyberShield-Lab` |

---

## 11.3 Project Implementation

During this project I configured and tested:

- Microsoft Hyper-V virtual machines
- Windows Server 2022
- Active Directory Domain Services (AD DS)
- DNS
- Organisational Units (OUs)
- Domain user accounts
- Global and Domain Local security groups
- AGDLP access-control design
- Windows 11 domain membership
- NTFS permissions
- SMB file sharing
- Departmental access controls
- Group Policy
- Windows Defender Firewall policies
- Password policies
- Account lockout policies
- User password resets
- Disabled and locked user accounts
- Active Directory troubleshooting
- DNS troubleshooting
- Group membership troubleshooting
- Windows security-token refresh behaviour
- Windows Server Backup
- File recovery
- Hyper-V virtual networking
- Network topology documentation

---

## 11.4 Active Directory Administration

A structured Active Directory environment was created using separate OUs for users, groups, computers, and servers.

Departmental users and security groups were created for areas including:

- IT
- HR
- Finance
- Sales

Access control was implemented using the **AGDLP** model:

**Accounts → Global Groups → Domain Local Groups → Permissions**

This provided practical experience with scalable Active Directory permission management rather than assigning permissions directly to individual users.

---

## 11.5 File Sharing and Permissions

Departmental file shares were configured and secured using a combination of:

- NTFS permissions
- Share permissions
- Active Directory security groups

Access was tested using different domain accounts to verify that authorised users could access departmental resources while unauthorised users were denied access.

This demonstrated the relationship between authentication, group membership, NTFS permissions, and SMB share permissions.

---

## 11.6 Group Policy and Security

Group Policy was used to centrally manage workstation security.

A workstation security GPO was created and linked to the appropriate computer OU.

Windows Defender Firewall settings were configured and verified on `CLIENT01`.

Domain password and account lockout policies were also configured, including:

- Minimum password length
- Password history
- Password age
- Account lockout threshold
- Lockout duration
- Lockout counter reset

These policies were validated through practical user logon and account-management tests.

---

## 11.7 Troubleshooting

Several realistic troubleshooting scenarios were performed rather than documenting only successful configurations.

These included:

- Incorrect DNS configuration
- Domain connectivity problems
- File-share access denial
- Missing security-group membership
- Departmental access changes
- Stale Windows logon security tokens

Tools and commands used during troubleshooting included:

- `ping`
- `nslookup`
- `ipconfig`
- `gpupdate`
- `gpresult`
- `net accounts`
- Active Directory Users and Computers
- Group Policy Management
- Windows networking tools

The troubleshooting exercises demonstrated a structured approach of identifying symptoms, checking configuration, finding the root cause, applying a fix, and validating the result.

---

## 11.8 Backup and Recovery

Windows Server Backup was installed and configured on `DC01`.

A dedicated virtual backup disk was created and used as the backup destination.

Departmental data was backed up and a recovery test was performed by:

1. Creating a test file.
2. Running a successful backup.
3. Deleting the test file.
4. Opening the Windows Server Backup Recovery Wizard.
5. Selecting the appropriate recovery point.
6. Restoring the deleted file.
7. Verifying successful recovery.

This demonstrated both backup configuration and practical recovery validation.

---

## 11.9 Network Documentation

A network topology was created using Cisco Packet Tracer to document the relationship between:

- Internet connection
- Home router
- Windows 11 Hyper-V host
- Hyper-V internal virtual network
- `DC01`
- `CLIENT01`

The Packet Tracer diagram provides a conceptual representation of the environment and is included in the repository together with the exported topology image.

---

## 11.10 Skills Demonstrated

This project demonstrates hands-on experience across several areas relevant to IT support and junior infrastructure roles.

### Windows Administration
- Windows Server 2022
- Windows 11 administration
- Active Directory administration
- User and group management
- Password resets
- Account unlocking and disabling

### Networking
- IPv4 addressing
- DNS configuration
- Connectivity testing
- Name resolution troubleshooting
- Hyper-V virtual networking
- Network topology documentation

### Security
- Group-based access control
- AGDLP
- NTFS permissions
- SMB share permissions
- Group Policy
- Windows Defender Firewall
- Password policies
- Account lockout policies
- Principle of least privilege

### Troubleshooting
- DNS troubleshooting
- Authentication troubleshooting
- Permission troubleshooting
- Group membership troubleshooting
- Group Policy validation
- Windows security-token troubleshooting

### Backup and Recovery
- Windows Server Backup
- Dedicated backup storage
- Backup validation
- File recovery testing

### Documentation
- GitHub project documentation
- Technical screenshots
- Configuration records
- Troubleshooting evidence
- Cisco Packet Tracer network diagrams

---

## 11.11 Key Learning Outcomes

Building the CyberShield lab provided practical experience beyond theoretical Active Directory knowledge.

The project demonstrated how DNS, authentication, security groups, permissions, Group Policy, networking, and Windows security mechanisms work together within a domain environment.

It also reinforced the importance of testing and validation. Configuration changes were not considered complete until their behaviour had been verified from the client or user perspective.

Troubleshooting scenarios helped develop a systematic approach to diagnosing IT problems by identifying symptoms, checking relevant configuration, isolating the cause, implementing a solution, and confirming successful resolution.

---

## 11.12 Project Outcome

The completed CyberShield Active Directory Lab provides a documented portfolio project demonstrating practical experience with Microsoft enterprise technologies and common IT administration tasks.

The environment can also be expanded in the future with additional Windows clients, servers, services, security controls, monitoring, automation, and further troubleshooting scenarios.
