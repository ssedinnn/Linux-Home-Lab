# Lab 4 - Linux File Permissions and Group-Based Access Control

## **Objective**

Learn how to configure and manage Linux file ownership, directory permissions, group-based access control, and advanced security permissions to protect shared resources in a simulated business environment.

## **Environment**

- Hypervisor / Virtualization: Oracle VirtualBox
- Server OS: Ubuntu Server 26.04.1 LTS
- Host OS: Windows
- Virtual Machine: Ubuntu Server #1
- Server Hostname: ubu-srv-01
- Administrator Account: labadmin
- Network Configuration: NAT (Network Address Translation)
- Remote Administration: OpenSSH Server

## **Skills Demonstrated**

## **Steps**


### *Step 1 - Create Department Groups and Employee Accounts*

![Department Group Creation](img/Department_Group_Creation.png)

![Employee Account Creation](img/Employee_Account_Creation.png)

![Department Group Membership Assignment](img/Department_Group_Membership_Assignment.png)

I began by creating a simulated business environment consisting of two departments: Accounting and IT Support. Each department would have its own group and two employee accounts, which would later be used to configure and test group-based file permissions and access restrictions.

First, I ran the following commands to check whether the department groups already existed:

```bash
getent group accounting
getent group itsupport
```

- **`getent group accounting`** – Checks whether the `accounting` group exists and displays its group information if found.
- **`getent group itsupport`** – Checks whether the `itsupport` group exists and displays its group information if found.

The results showed that the `itsupport` group already existed from Lab 03 with a GID of `1002`. However, the `accounting` group did not exist.

I then ran the following commands to create and verify the Accounting group:

```bash
sudo groupadd accounting
getent group accounting
```

- **`groupadd`** – Creates a new group on the Linux system.
- **`getent group accounting`** – Verifies that the Accounting group was successfully created.

The results confirmed that the `accounting` group was successfully created with a GID of `1003`.

Next, I created four user accounts to represent employees working in both departments:

```bash
sudo adduser accounting01
sudo adduser accounting02
sudo adduser itsupport01
sudo adduser itsupport02
```

- **`adduser`** – Creates a new user account, configures its home directory, and prompts the administrator to set a password.

For each employee account, I configured a password and left the optional personal information fields blank. These accounts were created as standard users without sudo group membership so that I could accurately test access restrictions later in the lab.

After creating the employee accounts, I assigned each user to their respective department group using the following commands:

```bash
sudo usermod -aG accounting accounting01
sudo usermod -aG accounting accounting02
sudo usermod -aG itsupport itsupport01
sudo usermod -aG itsupport itsupport02
```

- **`usermod`** – Modifies an existing user account.
- **`-a`** – Appends the user to additional supplementary groups without removing their existing group memberships.
- **`-G`** – Specifies the supplementary group or groups that the user should belong to.

I then ran the following commands to verify each employee's group memberships:

```bash
groups accounting01
groups accounting02
groups itsupport01
groups itsupport02
```

- **`groups`** – Displays the primary and supplementary groups that a specified user belongs to.

The results confirmed that both Accounting employees belonged to the `accounting` group and both IT Support employees belonged to the `itsupport` group. Each employee also retained their existing primary group and membership in the `users` group.

Finally, I verified the members of both department groups using the following commands:

```bash
getent group accounting
getent group itsupport
```

The results confirmed the following department group memberships:

| Department Group | GID | Members |
| --- | --- | --- |
| accounting | 1003 | accounting01, accounting02 |
| itsupport | 1002 | itsupport01, itsupport02 |

This step established the foundation for implementing group-based access control. In professional IT environments, administrators commonly organize employees into groups based on their departments or job responsibilities. This simplifies permission management by allowing administrators to assign access to an entire group rather than configuring permissions for each individual user.

These department groups and employee accounts will be used throughout the remainder of the lab to configure shared directories, manage file ownership, and test authorized and unauthorized access.

## **Challenges**

## **What I Learned**

## **Next Steps**
