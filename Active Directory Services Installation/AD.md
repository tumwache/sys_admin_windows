# Step-by-Step Guide: Installing Active Directory Services Using Windows Server 2025 on VMware Workstation

Active Directory (AD) is an essential component for managing identities, authentication, and authorization in Windows environments. This guide provides a comprehensive walkthrough for installing Active Directory Domain Services (AD DS) on **Windows Server 2025**, using **VMware Workstation** as the virtualization platform.

## Prerequisites

- **VMware Workstation** installed on your machine.
- A **Windows Server 2025** ISO image.
- A virtual machine created and Windows Server 2025 installed.
- Administrative privileges on the Windows Server.

## 1. Start Your Windows Server 2025 VM

1. Launch **VMware Workstation**.  
2. Power on your Windows Server 2025 virtual machine.  
3. Log in with an account that has administrator rights.

## 2. Open Server Manager

Once logged in, **Server Manager** usually opens automatically. If not, open it from the taskbar or start menu.

- **Tip:** Server Manager is your hub for managing server roles and features.

## 3. Start the Add Roles and Features Wizard

1. Click on the **"Manage"** menu at the top right.  
2. Select **"Add Roles and Features"** from the dropdown.

> This step launches the wizard that allows you to configure new roles and features for your server.

## 4. Choose Installation Type

1. On the welcome pane, click **Next**.  
2. Select **"Role-based or feature-based installation"** and click **Next**.

> This option allows you to install roles—including Active Directory Domain Services—on the local server.

## 5. Select Destination Server

1. The server you are currently working on will appear in the server pool.  
2. Ensure your local server is selected (it is by default), then click **Next**.

## 6. Select Server Roles

1. In the list of roles, scroll down and check **"Active Directory Domain Services"**.  
2. A pop-up will appear to add required features for AD DS. Click **Add Features**.  
3. Click **Next**.

> Active Directory Domain Services will enable your server to function as a domain controller.

## 7. Add Features

1. On the **Features** screen, you can accept the defaults unless you have specific needs.  
2. Click **Next**.

## 8. Review and Confirm Installation

1. A summary of your selections is displayed.  
2. Optionally, check **"Restart the destination server automatically if required"**.  
3. Click **Install**.

> The installation process will begin; wait for it to complete.

## 9. Promote Server to Domain Controller

Once the installation finishes, a yellow exclamation mark notification will appear at the top of Server Manager.

1. Click on the **flag notification** and then on the link: **"Promote this server to a domain controller"**.

## 10. Deploy a New Forest

1. In the **Deployment Configuration** window, select **"Add a new forest"**.  
2. Enter your desired **root domain name** (e.g., `mydomain.local`).  
3. Click **Next**.

## 11. Specify Domain Controller Options

1. Set the required **Domain Controller Capabilities** (DNS, GC, etc.).  
2. Enter and confirm a **Directory Services Restore Mode (DSRM)** password.  
3. Click **Next**.

## 12. Configure DNS Options

- If you selected to install DNS, accept defaults or provide settings as needed.  
- Click **Next**.

## 13. Additional Options & Paths

1. NetBIOS name will auto-fill, but can be changed if required.  
2. Set database, log, and SYSVOL folder locations (defaults are usually recommended).  
3. Click **Next**.

## 14. Review and Install

1. Review all configuration selections.  
2. Click **Next**, then click **Install**.

> The server will now be promoted to a domain controller and will restart upon completion.

## 15. Confirm AD DS Installation

Once the server restarts:

1. Log in using your **domain credentials**.  
2. Open **Server Manager** and ensure the AD DS role is present and healthy.  
3. The server now acts as a **domain controller** for your new domain.

## Troubleshooting Tips

- Ensure networking is properly configured in VMware so your VM can communicate.  
- If issues arise during promotion, review logs in the **C:\Windows\NTDS** and use **Event Viewer**.

## Next Steps

- Join domain clients to your new AD domain.  
- Manage users, groups, and organizational units from **Active Directory Users and Computers**.  
- Explore advanced features like Group Policy and DNS management.

**This guide provides a reliable foundation for new or experienced administrators deploying Active Directory Domain Services on Windows Server 2025 in a VMware environment.**
