
# Step-by-Step Guide to Active Directory Users and Computers (ADUC)

## Introduction and Key Concepts

This guide walks you through managing core Active Directory (AD) objects using **Active Directory Users and Computers (ADUC)** on Windows Server. It is structured chronologically for hands-on execution and includes definitions and practical insights for each object.

### Key Definitions

- **Users**: Security principals representing people or services that need access to resources. Users authenticate to the domain to gain access, and their attributes (such as group membership, profile path, and password policies) control their permissions.

- **Computers**: AD objects representing domain-joined machines (servers, workstations). Each computer has its own account and can be targeted by policies, auditing, and access controls.

- **Domain Controllers (DCs)**: Servers that host the AD database (the directory) and provide authentication, replication, and directory services for the domain. They validate credentials, process logons, and replicate changes to other DCs.

- **Organizational Units (OUs)**: Containers used to organize and delegate administration of AD objects (users, computers, groups). OUs can host Group Policy links and support granular delegation without affecting the entire domain.

- **Group Policy**: A centralized mechanism to configure and enforce settings (security, desktop configuration, software deployment, etc.) for users and computers. Group Policy Objects (GPOs) can be linked to sites, domains, or OUs to apply in hierarchical order.

---

## Prerequisites

1. Windows Server joined to the domain or acting as a Domain Controller.
2. You have appropriate privileges (typically Domain Admins or delegated rights).
3. Active Directory Domain Services role installed (if managing on a DC or admin workstation).
4. ADUC console available (via `dsa.msc` or **Server Manager > Tools > Active Directory Users and Computers**).

---

## 1. Launching Active Directory Users and Computers

1. Log into a domain-joined administrative workstation or Domain Controller.
2. Open **Server Manager**.
3. Navigate to **Tools > Active Directory Users and Computers**.
   - Alternatively, press `Win + R`, type `dsa.msc`, and press Enter.
4. Expand your domain in the left pane to expose containers like **Users**, **Computers**, **Domain Controllers**, and any existing **OUs**.

---

## 2. Managing Users

### Create a New User

1. In ADUC, expand your domain and click on the **Users** container (or a designated OU if following delegation/naming).
2. Right-click > **New > User**.
3. Fill in:
   - **First name**, **Last name**
   - **User logon name** (sAMAccountName / UPN)
4. Click **Next** and set the password.
5. Choose password options:
   - User must change password at next logon
   - Password never expires (use cautiously)
   - Account is disabled (if creating ahead)
6. Click **Finish**.

### Manage User Properties

1. Right-click the created user > **Properties**.
2. Explore tabs (General, Account, Profile, Member Of, etc.)
   - Add the user to security or distribution groups under **Member Of**.
   - Set login hours, account expiration, or configure profile paths.

### Resetting a User Password

1. Right-click the user > **Reset Password**.
2. Provide a new password and configure the checkboxes (e.g., require change at next logon).
3. Click **OK**.

### Best Practices for Users

- Use consistent naming conventions (e.g., `firstname.lastname` or `initialsLastname`).
- Avoid placing all users in the default **Users** container; create departmental OUs.
- Use security groups for permission assignment instead of individual user rights.

---

## 3. Managing Computers

### Pre-staging a Computer Account (Optional)

1. Right-click the **Computers** container or OU where computer accounts belong.
2. Select **New > Computer**.
3. Enter the computer name (must match the actual machine name).
4. Optionally assign the computer to a user or set delegation.

### Joining a Computer to the Domain

(On the client/workstation side:)

1. Open **System Properties** > **Computer Name** > **Change**.
2. Select **Domain** and enter your domain name.
3. Provide domain credentials with privileges to join computers.
4. Restart the computer.
5. The computer account appears in ADUC under **Computers** or the targeted OU.

### Managing Computer Properties

1. Right-click the computer object > **Properties**.
2. View and modify description, managed by, or delegation settings.

### Best Practices for Computers

- Place computer objects in OUs aligned to their function (e.g., `Workstations`, `Servers`).
- Use Group Policy filtering and WMI if granular targeting is needed.
- Pre-stage accounts for sensitive or locked-down environments.

---

## 4. Domain Controllers

1. In ADUC, click the **Domain Controllers** container.
2. This lists all domain controllers in the domain (e.g., `DC1`, `DC2`).
3. Right-click a domain controller > **Properties** to view:
   - NTDS settings (replication metadata)
   - Operating system version
   - Managed by attribute

### Common Administrative Tasks

- **Seizing or transferring FSMO roles** is done via specific tools (e.g., `ntdsutil`, `Active Directory Users and Computers` for certain roles).
- **Verifying replication**: Use `repadmin /replsummary` on a DC to confirm health.
- Domain controllers should be in secure OUs and monitored separately.

---

## 5. Organizational Units (OUs)

### Create an OU

1. Right-click the domain (or parent OU) > **New > Organizational Unit**.
2. Provide a name (e.g., `HR`, `IT-Workstations`, `Servers`).
3. Optionally check **Protect container from accidental deletion** (recommended).

### Delegating Control

1. Right-click the OU > **Delegate Control...**
2. Use the **Delegation of Control Wizard** to:
   - Add a user or group.
   - Choose predefined tasks (create/delete user, reset password) or custom tasks.
3. Finish the wizard to grant scoped permissions without elevating to domain-wide rights.

### Best Practices

- Reflect organizational structure in OUs, but avoid over-nesting.
- Use OUs to scope Group Policy application cleanly.
- Protect critical OUs from accidental deletion.

---

## 6. Group Policy Basics via ADUC Context

While Group Policy Objects (GPOs) are typically managed via **Group Policy Management Console (GPMC)**, ADUC plays a role in understanding scope:

1. **Linking GPOs**: GPOs are linked to OUs, domains, or sites to apply settings to users/computers within them.
2. **Scope Awareness**: The placement of users and computers in OUs determines which GPOs apply.
3. **Security Filtering**: Use security group membership to filter GPO application further.

> For full GPO creation and editing, open **Group Policy Management** (`gpmc.msc`), create a GPO, edit settings, and link it to the appropriate OU. Then, ensure your users/computers reside in that OU or group.

---

## 7. Common Tasks & Workflow (Chronological)

1. Plan your OU structure to reflect administration and policy needs.
2. Create OUs and delegate control for local admins.
3. Create users in their respective OUs and assign to groups.
4. Pre-stage or join computers into their OUs.
5. Link GPOs to OUs for baseline security/configuration.
6. Monitor Domain Controllers for replication and health.
7. Adjust and troubleshoot using properties, group membership, and policy results (`gpresult` on client machines).

---

## 8. Tips, Tricks, and Best Practices

- **Avoid overloading the default containers**; customize and migrate objects into delegated OUs.
- **Use groups** (security group nesting) for scalable permission management.
- **Document your naming conventions** for users, computers, and OUs.
- **Enable auditing** for critical changes (user creation/deletion, OU changes).
- **Regularly review** inactive accounts and stale computer objects.
- **Use `Active Directory Administrative Center` alongside ADUC** for advanced tasks like fine-grained password policies or Active Directory Recycle Bin (if enabled).

---

## Conclusion

Active Directory Users and Computers is the foundational interface for daily directory management. When used with thoughtful OU design, delegation, and Group Policy placement, it becomes a precise instrument for scalable, secure identity and endpoint administration. This guide gives you the core operational steps; the next layer is automation (PowerShell) and monitoring (health checks and audit logs).
