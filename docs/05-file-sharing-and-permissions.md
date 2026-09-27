# 05 - File Sharing, NTFS Permissions & AGDLP Validation

This section documents the implementation and testing of departmental file sharing within the CyberShield Active Directory lab.

Departmental folders were created on `DC01` and secured using a combination of Active Directory security groups, NTFS permissions, and SMB share permissions.

The configuration completes the AGDLP permission model established earlier in the project:

**Accounts → Global Groups → Domain Local Groups → Permissions**

Access was then tested from the domain-joined Windows 11 workstation `CLIENT01` using users from different departments to verify both authorised access and departmental isolation.

## Departmental Folder Structure

A central data directory was created on `DC01`:

`C:\CyberShield-Data`

Four departmental folders were created:

- `Finance`
- `HR`
- `IT`
- `Sales`

This structure provides separate locations where access can be controlled according to departmental Active Directory group membership.

![Departmental Folder Structure](screenshots/file-sharing/01-departmental-folder-structure.png)

