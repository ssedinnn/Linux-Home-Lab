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

## **Challenges**

## **What I Learned**

## **Next Steps**

