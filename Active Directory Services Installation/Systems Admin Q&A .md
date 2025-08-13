# Windows System Administration – Complete Q&A Guide

This guide is part of the **sys_admin_windows** repository.  
It is designed to help learners, interview candidates, and working professionals quickly understand core Windows Server concepts — from beginner to advanced — while aligning with real-world system administration tasks.

---

## L1 – Basic Questions (Foundations)

1. **What is Active Directory (AD)?**  
   Microsoft’s directory service for centralized management of users, computers, groups, and resources in a network.

2. **What is DNS?**  
   The Domain Name System resolves domain names into IP addresses so computers can locate each other on the network.

3. **What is DHCP?**  
   The Dynamic Host Configuration Protocol automatically assigns IP addresses and other network configuration settings.

4. **What is a Domain Controller (DC)?**  
   A Windows Server that runs Active Directory Domain Services and handles authentication, authorization, and directory management.

5. **What is Group Policy?**  
   A centralized management tool for configuring user and computer settings in an Active Directory environment.

6. **What is NTFS?**  
   A secure and feature-rich file system supporting permissions, encryption, quotas, and large file sizes.

7. **What is RDP?**  
   Remote Desktop Protocol enables administrators and users to connect to and control a computer remotely.

8. **How to check system uptime?**  
   - Command Prompt: `systeminfo`  
   - Task Manager: Performance tab → “Up Time”

9. **What is Event Viewer?**  
   A Windows utility for viewing system, application, and security logs.

10. **Workgroup vs Domain – Difference?**  
    - **Workgroup**: Local management, no centralized control.  
    - **Domain**: Centralized management with unified credentials.

---

## L2 – Intermediate Questions (Operational Knowledge)

1. **What are FSMO Roles?**  
   Flexible Single Master Operations roles: Schema Master, Domain Naming Master, RID Master, PDC Emulator, Infrastructure Master.

2. **What is Active Directory Replication?**  
   The process of synchronizing AD data across Domain Controllers to ensure consistency.

3. **What is an OU (Organizational Unit)?**  
   A logical container in AD for grouping and managing objects.

4. **How to manage Windows Updates?**  
   - Use WSUS for centralized patching  
   - Configure via Group Policy

5. **What is Windows Failover Clustering?**  
   A high-availability feature allowing multiple servers to work together to minimize downtime.

6. **What is DNS Forwarding?**  
   Configuring a DNS server to forward unresolved queries to another DNS server.

7. **How to troubleshoot account lockouts?**  
   Check Event Viewer logs, identify failed logon sources, investigate mapped drives or services using old credentials.

8. **What is GPO Inheritance?**  
   Lower-level OUs inherit policies from higher-level containers unless blocked.

9. **How to use Task Scheduler?**  
   Automates scripts or programs to run on specific triggers.

10. **What is Shadow Copy?**  
    Creates point-in-time copies of files/folders for quick restoration.

---

## L3 – Advanced Questions (Real-World Skills)

### **Windows Server Installation**
1. **What are the main editions of Windows Server and how do they differ?**  
   - **Standard**: Full features but limited virtualization rights.  
   - **Datacenter**: Unlimited virtualization, advanced features.  
   - **Essentials**: Designed for small businesses, limited roles.

2. **What are post-installation configuration best practices?**  
   - Rename the server  
   - Configure static IP  
   - Join domain (if applicable)  
   - Enable firewall & security settings  
   - Apply latest updates

---

### **Active Directory Domain Services**
3. **What is the difference between a forest and a domain?**  
   - **Domain**: Logical group of objects sharing a database and policies.  
   - **Forest**: Collection of domains sharing a common schema and trust relationships.

4. **How do you add a new Domain Controller?**  
   Install AD DS role → Promote to DC via Server Manager → Configure replication.

5. **What is the Global Catalog?**  
   A DC role that stores partial attribute copies of all objects to speed up searches.

---

### **Organizational Units & Group Policy**
6. **Why use OUs?**  
   For logical grouping, delegation, and targeted Group Policy application.

7. **How do you block GPO inheritance?**  
   Right-click OU → Select “Block Inheritance.”

---

### **Users & Groups Management**
8. **Difference between security and distribution groups?**  
   - **Security**: Used for permissions.  
   - **Distribution**: Used for email distribution lists.

9. **How to disable vs delete a user account?**  
   - **Disable**: Prevents login but retains account data.  
   - **Delete**: Removes the account entirely.

---

### **Windows Clients: Domain Join**
10. **Common causes of domain join failure?**  
    - Network connectivity issues  
    - Incorrect DNS settings  
    - Time synchronization problems

---

### **File Shares & Permissions**
11. **NTFS permissions vs Share permissions?**  
    - **NTFS**: File system-level, more granular.  
    - **Share**: Network-level, applies to all network users.

12. **What is permission inheritance?**  
    Objects inherit permissions from their parent unless explicitly changed.

---

### **Backup & Disaster Recovery**
13. **What are the main backup types in Windows Server?**  
    - Full  
    - Incremental  
    - Differential

14. **What is the Windows Server Backup tool?**  
    A built-in utility for scheduling and restoring server backups.

---

### **PowerShell Automation**
15. **How to create a user via PowerShell?**  
    ```powershell
    New-ADUser -Name "John Doe" -SamAccountName jdoe -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) -Enabled $true
    ```

16. **How to list all installed roles and features?**  
    ```powershell
    Get-WindowsFeature
    ```

---

> **Tip:** This Q&A file should be used alongside the lab guides in each folder of the repository for hands-on practice.
