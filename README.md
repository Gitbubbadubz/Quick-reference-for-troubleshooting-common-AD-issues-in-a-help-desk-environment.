# Quick-reference-for-troubleshooting-common-AD-issues-in-a-help-desk-environment.
AD Quick Reference Guide

1. Basic Active Directory Tasks
A. User Account Management
Task	                                  Steps
Reset Password:	            Right-click user > Reset Password (Enforce change at next logon)
Unlock Account:	            Right-click user > Unlock Account
Disable/Enable Account:	    Right-click user > Disable/Enable
Create New User:	          Right-click OU > New > User (Fill in details, set password)

B. Group Management
Task	                                 Steps
Add User to Group:	        Right-click group > Properties > Members > Add
Remove User from Group:	    Select user in group > Remove
Create New Group:         	Right-click OU > New > Group (Security/Distribution)

2. Common AD Issues & Fixes
A. "Account Locked Out"
✅ Steps to Resolve:
   1: Unlock account (see above).
   2: Check lockout source:
        PowerShell   Get-ADUser -Identity "username" -Properties LockedOut,LastBadPasswordAttempt

B. "Password Expired"
✅ Steps to Resolve:

  1.Reset password (see above).
  2.Extend password expiration (if policy allows):
       PowerShell  Set-ADUser -Identity "username" -PasswordNeverExpires $true         ``` *(Use cautiously!)*  
       
C. "User Cannot Log In (Access Denied)"
✅ Steps to Resolve:

 1.Check group memberships (Ensure user has proper permissions).
 2.Verify OU permissions (Check inheritance blocking).
 3.Test on another PC (Rule out workstation-specific issues).

D. Broken Trust Relationship (PC Won’t Authenticate)
✅ Steps to Resolve:

 1.Remove PC from domain (Local admin required).
 2.Rejoin domain (System Properties > Change > Rejoin domain).

3. Help Desk Best Practices
✔ Always document changes (Ticket notes, AD comments).
✔ Verify user identity (Prevent social engineering).
✔ Escalate complex issues (FSMO roles, schema changes).

5 Useful PowerShell Commands
    Command	                                Purpose
Get-ADUser -Filter *	                 List all AD users
Search-ADAccount -LockedOut	           Find all locked accounts
Get-ADComputer -Filter *	             List all domain-joined PCs
Test-ComputerSecureChannel -Repair	   Fix trust relationship

Quick Reference Cheat Sheet
📌 Common AD Tools:

Active Directory Users & Computers (ADUC) – User/group management.

Active Directory Administrative Center (ADAC) – Modern AD management.

Event Viewer – Check security/authentication logs.

📌 Common Event IDs:

4625 – Failed login

4740 – Account locked out

4768 – Kerberos auth failure







