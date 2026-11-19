# Lab 3 - Linux User and Group Management

## **Objective**

## **Environment**

## **Skills Demonstrated**

## **Steps**


### Step 1 – Examining Existing Users and Groups

![Checking Current User and Groups](img/Checking_Current_User_and_Groups.png)

![Checking User and Group Info](img/Checking_User_and_Group_Info.png)

I began by examining the existing user account and group memberships on my Ubuntu Server. Before creating or managing additional users, I wanted to understand how Linux identifies users, assigns group memberships, and stores account information.

First, I ran the following commands to identify my current user and examine its group memberships:

```bash
whoami
id
groups
```

- **`whoami`** – Displays the username of the account currently logged into the system. In my case, the command returned `labadmin`.
- **`id`** – Displays information about the current user, including their User ID (UID), primary Group ID (GID), and supplementary group memberships.
- **`groups`** – Lists the groups that the current user belongs to.

The `id` command showed that my `labadmin` account has a UID of `1000` and a primary GID of `1000`. It also showed several supplementary groups, including `sudo`, which allows authorized users to perform administrative tasks.

Next, I used the following commands to examine how Linux stores user and group information:

```bash
getent passwd labadmin
getent group sudo
```

- **`getent`** – Retrieves entries from system databases, including user accounts and groups.
- **`getent passwd labadmin`** – Displays account information for `labadmin`, including its UID, GID, home directory, and default shell.
- **`getent group sudo`** – Displays information about the `sudo` group, including its GID and listed members.

The `getent passwd labadmin` command returned information showing that my account uses `/home/labadmin` as its home directory and `/bin/bash` as its default shell.

The `getent group sudo` command confirmed that `labadmin` is a member of the `sudo` group, which provides administrative privileges through the `sudo` command.

This step helped me understand how Linux identifies user accounts and organizes permissions through group memberships. It also introduced me to the difference between a user's primary group and supplementary groups, which will be important when creating and managing additional accounts.


### Step 2 – Creating a New Linux User Account

![Creating and Verifying a New Linux User](img/Creating_and_Verifying_a_Linux_User.png)

In this step, I practiced creating a new Linux user account and verifying its information. User account creation is a common administrative task when setting up access for new employees or managing accounts on a Linux server.

First, I created a new user named `testuser` using the following command:

```bash
sudo adduser testuser
```

- **`sudo`** – Executes the command with administrative privileges.
- **`adduser`** – Creates a new Linux user account and automatically sets up its home directory and primary group.
- **`testuser`** – The username assigned to the new account.

After running the command, I was prompted to create and confirm a password for the new user. I left the optional personal information fields blank and confirmed the account creation.

Next, I verified that the account was successfully created:

```bash
getent passwd testuser
```

This command retrieves the account information for `testuser`, including its UID, GID, home directory, and default login shell.

The output confirmed that `testuser` was assigned a UID and primary GID of `1001`, a home directory of `/home/testuser`, and `/bin/bash` as its default shell.

I then examined the new user's group memberships:

```bash
id testuser
groups testuser
```

- **`id testuser`** – Displays the user's UID, primary GID, and supplementary group memberships.
- **`groups testuser`** – Lists the groups that the user belongs to.

The results showed that `testuser` belongs to its primary group, `testuser`, and the supplementary `users` group. Unlike my `labadmin` account, the new user was not assigned to the `sudo` group, meaning it does not have administrative privileges through the default sudo group configuration.

Finally, I verified that the user's home directory was created:

```bash
ls -ld /home/testuser
```

- **`ls -l`** – Displays detailed information about files and directories, including permissions and ownership.
- **`-d`** – Displays information about the directory itself rather than listing its contents.

The output confirmed that `/home/testuser` was successfully created and that both its owner and group were assigned to `testuser`.

**Challenge Encountered:**

When initially running `sudo adduser testuser`, I entered my administrator password incorrectly, resulting in an authentication failure. I retried the command, entered the correct password, and successfully created the account.

This step helped me understand how Linux administrators create user accounts, assign passwords, verify account information, and examine group memberships and home directory ownership.

## **Challenges**

## **What I Learned**

## **Next Steps**

