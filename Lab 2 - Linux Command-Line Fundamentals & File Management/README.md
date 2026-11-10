# Lab 2 - Linux Command-Line Fundamentals & File Management

## **Objective**

Learn how to navigate the Linux filesystem and manage files and directories using terminal commands. This lab focuses on understanding the Linux directory structure, creating and organizing files, viewing file contents, copying and moving files, and safely deleting files and directories.

## **Environment**

- **Hypervisor / Virtualization:** Oracle VirtualBox
- **Server OS:** Ubuntu Server 26.04.1 LTS
- **Host OS:** Windows
- **Virtual Machine:** Ubuntu Server #1
- **Server Hostname:** `ubu-srv-01`
- **Administrator Account:** `labadmin`
- **Network Configuration:** NAT (Network Address Translation)
- **Remote Administration:** OpenSSH Server

## **Skills Demonstrated**

## **Steps**

### *Step 1 - Explore the Linux Filesystem*

![Linux Filesystem Navigation](img/Linux_Filesystem_Navigation.png)

In the Ubuntu Server VM, I begin by exploring the Linux filesystem using basic terminal commands. Since Ubuntu Server does not include a graphical desktop interface by default, I use the command-line interface to navigate between directories and view their contents.

I first use the following command:

```bash
pwd
```

The `pwd` command stands for **Print Working Directory**. It displays the absolute path of the directory I am currently working in.

The command returns:

```text
/home/labadmin
```

This confirms that I am currently in the home directory of the `labadmin` user. In Linux, regular user home directories are typically located under `/home`, with each user having their own directory for personal files and configurations.

Next, I use:

```bash
ls
```

The `ls` command lists the files and directories within the current working directory. In this case, the command does not display any files because there are no visible files or directories in my home directory.

However, Linux also contains hidden files that are not displayed by the standard `ls` command.

To view these files and additional information, I use:

```bash
ls -la
```

This command combines two options:

- `-l` — Displays files and directories in a detailed listing format, including permissions, ownership, file size, and modification date.
- `-a` — Displays all files and directories, including hidden files whose names begin with a period (`.`).

The output displays several hidden files and directories, including:

- `.bashrc` — Contains Bash shell configuration settings and commands that are typically executed when starting an interactive Bash shell.
- `.profile` — Contains user environment settings and commands that may be executed during login.
- `.bash_logout` — Contains commands that Bash may execute when exiting a login shell.
- `.cache` — Stores cached application data.
- `.ssh` — Commonly stores SSH configuration files, authentication keys, and known host information.

The output also includes `.` and `..`, which represent the current directory and its parent directory.

Next, I navigate to another directory using:

```bash
cd /etc
```

The `cd` command stands for **Change Directory** and allows me to move between directories in the Linux filesystem.

The `/etc` directory contains system-wide configuration files used by the operating system, services, and installed applications.

After changing directories, I use:

```bash
pwd
```

The command returns:

```text
/etc
```

This confirms that I successfully navigated from my home directory to `/etc`.

I then use:

```bash
ls
```

This displays the files and directories located inside `/etc`, including configuration files and directories associated with networking, authentication, system services, and other operating system components.

Some examples visible in the output include:

- `hostname` — Stores the system's configured hostname.
- `hosts` — Contains local hostname-to-IP address mappings.
- `ssh` — Contains system-wide SSH configuration files.
- `netplan` — Contains network configuration files used by Netplan.
- `apt` — Contains configuration files and repository settings for Ubuntu's APT package manager.

Finally, I return to my home directory using:

```bash
cd ~
```

The `~` symbol represents the current user's home directory. Using `cd ~` allows me to return to my home directory without typing the complete path.

To verify my location, I use:

```bash
pwd
```

The command returns:

```text
/home/labadmin
```

This confirms that I successfully returned to my home directory.

This step demonstrates how to navigate the Linux filesystem using terminal commands, identify hidden files, inspect directory contents, and understand the difference between user directories and system configuration directories.

### *Step 2 - Create Directories*

![Linux Directory Creation](img/Linux_Directory_Creation.png)

In the Ubuntu Server VM, I begin creating a directory structure that I will use to practice Linux file management throughout the remaining steps of this lab.

I first use the following command:

```bash
mkdir LinuxPractice
```

The `mkdir` command stands for **Make Directory** and is used to create new directories in Linux.

In this case, the command creates a directory named `LinuxPractice` inside my current working directory, which is `/home/labadmin`.

Next, I navigate into the newly created directory using:

```bash
cd LinuxPractice
```

The `cd` command stands for **Change Directory** and allows me to navigate between directories in the Linux filesystem.

After running the command, my terminal prompt changes to:

`labadmin@ubu-srv-01:~/LinuxPractice$`

This confirms that I am now working inside the `LinuxPractice` directory. The `~` symbol represents my home directory, so the full path is `/home/labadmin/LinuxPractice`.

Next, I create three additional directories using:

```bash
mkdir Documents Scripts Backups
```

The `mkdir` command can create multiple directories at once by specifying each directory name separated by a space.

This command creates three directories inside `LinuxPractice`:

- `Documents` — A directory for storing and practicing with text files.
- `Scripts` — A directory that can be used to organize scripts and other files.
- `Backups` — A directory for storing copies of files during future file management exercises.

Finally, I verify that the directories were successfully created using:

```bash
ls
```

The `ls` command lists the contents of the current working directory.

The output displays:

```text
Backups  Documents  Scripts
```

This confirms that all three directories were successfully created inside `LinuxPractice`.

The resulting directory structure is:

```text
/home/labadmin/
└── LinuxPractice/
    ├── Backups/
    ├── Documents/
    └── Scripts/
```

This step demonstrates how to create directories using `mkdir`, navigate between directories using `cd`, and verify directory creation using `ls`. It also shows how multiple directories can be created using a single command.


### *Step 3 - Create and View Files*

![Linux File Creation](img/Linux_File_Creation.png)

In the Ubuntu Server VM, I begin practicing how to create and manage files using Linux terminal commands. After creating the `LinuxPractice` directory structure in the previous step, I navigate into the `Documents` directory to begin working with text files.

I first use the following command:

```bash
cd ~/LinuxPractice/Documents
```

The `cd` command allows me to change my current working directory. Instead of navigating through each directory individually, I specify the path to the `Documents` directory.

The `~` symbol represents my home directory, `/home/labadmin`, allowing me to navigate directly to `/home/labadmin/LinuxPractice/Documents`.

Next, I create two empty text files using:

```bash
touch notes.txt tasks.txt
```

The `touch` command is used to update a file's access and modification timestamps. If the specified file does not already exist, `touch` creates a new empty file.

In this case, I use `touch` to create two files:

- `notes.txt` — A text file that I will use to practice writing and reading file contents.
- `tasks.txt` — An additional text file that I will use in future file management exercises.

The `.txt` extension indicates that these files are intended to contain plain text. Unlike Windows, Linux does not require a file extension to identify or work with a file.

I can also create multiple files using a single `touch` command by separating their filenames with spaces.

Next, I write text into `notes.txt` using:

```bash
echo "Learning Linux file management" > notes.txt
```

The `echo` command displays text or variable values in the terminal. However, in this command, I use the output redirection operator (`>`) to send the text into a file instead of displaying it on the screen.

The command consists of three parts:

- `echo` — Produces the text specified after the command.
- `"Learning Linux file management"` — The text that I want to write into the file.
- `> notes.txt` — Redirects the output into the `notes.txt` file.

The `>` operator creates the destination file if it does not exist or **overwrites its existing contents** if it already exists.

This means that running another command using `> notes.txt` would replace the previous text rather than add to it.

To add new text without overwriting the existing contents, I could instead use the append operator (`>>`):

```bash
echo "Practicing Linux commands" >> notes.txt
```

The `>>` operator appends the new text to the end of the file while preserving its existing contents.

After writing text into `notes.txt`, I verify the file's contents using:

```bash
cat notes.txt
```

The `cat` command stands for **Concatenate** and is commonly used to display the contents of text files directly in the terminal.

Although `cat` can also combine multiple files, I use it here to read the contents of a single file.

The command returns:

```text
Learning Linux file management
```

This confirms that the text was successfully written into `notes.txt` using the `echo` command and output redirection.

This step demonstrates how to create empty files using `touch`, write text into files using `echo` and output redirection, and display file contents using `cat`. It also introduces the difference between overwriting file contents with `>` and appending text with `>>`.


### *Step 4 - Copy Files and Directories*

![Linux File Copy](img/Linux_File_Copy.png)

In the Ubuntu Server VM, I begin practicing how to copy files and directories using Linux terminal commands. Copying files is an important system administration task because it allows administrators to create backups, duplicate configuration files, and preserve important data before making changes.

I first navigate to the `Documents` directory using:

```bash
cd ~/LinuxPractice/Documents
```

This places me inside the directory containing the `notes.txt` and `tasks.txt` files created in Step 3.

Next, I create a copy of `notes.txt` using:

```bash
cp notes.txt notes_backup.txt
```

The `cp` command stands for **Copy** and is used to copy files and directories in Linux.

The basic syntax is:

```bash
cp source destination
```

In this case:

- `cp` — Executes the copy operation.
- `notes.txt` — The original file being copied.
- `notes_backup.txt` — The destination filename for the copied file.

Unlike the `mv` command, which moves or renames files, `cp` preserves the original file while creating a separate copy.

I then verify that the copy was created using:

```bash
ls
```

The output displays:

```text
notes.txt  notes_backup.txt  tasks.txt
```

This confirms that the original file and its copy exist within the same directory.

Next, I copy `notes.txt` into the `Backups` directory created in Step 2:

```bash
cp notes.txt ../Backups/
```

This command introduces the use of **relative paths** when copying files between directories.

The command consists of the following components:

- `cp` — Copies the specified file.
- `notes.txt` — The source file located in my current directory.
- `..` — Represents the parent directory of my current working directory.
- `../Backups/` — Specifies the `Backups` directory located one level above `Documents`.

Since I am currently working inside `/home/labadmin/LinuxPractice/Documents`, the `..` notation refers to `/home/labadmin/LinuxPractice`.

Linux then uses the remaining path, `Backups/`, to locate the destination directory.

To verify that the file was copied successfully, I run:

```bash
ls ../Backups
```

The output displays:

```text
notes.txt
```

This confirms that the file was successfully copied into the `Backups` directory.

I also verify that the copied file contains the original text using:

```bash
cat ../Backups/notes.txt
```

The command returns:

```text
Learning Linux file management
```

This confirms that the contents of the original file were preserved during the copying process.

Next, I return to the main `LinuxPractice` directory using:

```bash
cd ~/LinuxPractice
```

I then create a complete copy of the `Documents` directory using:

```bash
cp -r Documents DocumentsBackup
```

This command introduces the **recursive (`-r`) option**.

By default, the `cp` command copies individual files. To copy an entire directory and its contents, I use the `-r` option.

The command consists of:

- `cp` — Executes the copy operation.
- `-r` — Recursively copies the directory and everything inside it, including any subdirectories.
- `Documents` — The source directory being copied.
- `DocumentsBackup` — The destination directory that will contain the copied files.

Because `DocumentsBackup` does not already exist, Linux creates it and copies the contents of `Documents` into it.

Finally, I verify the copied directory using:

```bash
ls DocumentsBackup
```

The output displays:

```text
notes.txt  notes_backup.txt  tasks.txt
```

This confirms that the `Documents` directory and all three files were successfully copied into `DocumentsBackup`.

The resulting directory structure is:

```text
LinuxPractice/
├── Backups/
│   └── notes.txt
├── Documents/
│   ├── notes.txt
│   ├── notes_backup.txt
│   └── tasks.txt
├── DocumentsBackup/
│   ├── notes.txt
│   ├── notes_backup.txt
│   └── tasks.txt
└── Scripts/
```

This step demonstrates how to copy individual files using `cp`, copy files between directories using relative paths, verify copied file contents using `cat`, and recursively copy entire directories using `cp -r`.

These operations are useful in Linux system administration when backing up files, duplicating directories, and preserving configurations before making changes.


### *Step 5 - Move and Rename Files*

![Linux File Rename and Move](img/Linux_File_Rename_and_Move.png)

In the Ubuntu Server VM, I begin practicing how to move and rename files using Linux terminal commands. Moving and renaming files is an important system administration task because it allows administrators to organize directories, relocate files, and manage system resources without creating unnecessary copies.

I first navigate to the `Documents` directory using:

```bash
cd ~/LinuxPractice/Documents
```

I then use the `ls` command to verify that the files created in the previous steps are still present.

The output displays:

```text
notes.txt  notes_backup.txt  tasks.txt
```

Next, I rename the `tasks.txt` file using:

```bash
mv tasks.txt todo.txt
```

The `mv` command stands for **Move** and is used to move or rename files and directories in Linux.

The basic syntax is:

```bash
mv source destination
```

The command consists of the following components:

- `mv` — Executes the move or rename operation.
- `tasks.txt` — The original filename.
- `todo.txt` — The new filename.

Because both filenames refer to the same directory, the command renames `tasks.txt` to `todo.txt` without moving it to another directory.

Unlike the `cp` command introduced in Step 4, which creates a separate copy of a file, `mv` changes the file's name or location without intentionally creating an additional copy.

To verify that the file was renamed successfully, I run:

```bash
ls
```

The output displays:

```text
notes.txt  notes_backup.txt  todo.txt
```

This confirms that `tasks.txt` has been renamed to `todo.txt`, while the other files remain unchanged.

Next, I move the renamed file from the `Documents` directory into the `Scripts` directory created in Step 2.

I use the following command:

```bash
mv todo.txt ../Scripts/
```

This command uses a relative path to move the file into another directory.

The command consists of:

- `mv` — Moves the specified file.
- `todo.txt` — The source file located in the current directory.
- `..` — Represents the parent directory of the current working directory.
- `../Scripts/` — Specifies the `Scripts` directory located inside the parent directory.

Since I am currently working inside `/home/labadmin/LinuxPractice/Documents`, the `..` notation refers to `/home/labadmin/LinuxPractice`.

Linux then uses the remaining path, `Scripts/`, to locate the destination directory.

After moving the file, I use:

```bash
ls
```

The output displays:

```text
notes.txt  notes_backup.txt
```

This confirms that `todo.txt` is no longer located inside the `Documents` directory.

Finally, I verify that the file was successfully moved into the `Scripts` directory using:

```bash
ls ../Scripts
```

The output displays:

```text
todo.txt
```

This confirms that `todo.txt` was successfully moved from `Documents` into `Scripts`.

The resulting directory structure is:

```text
LinuxPractice/
├── Backups/
│   └── notes.txt
├── Documents/
│   ├── notes.txt
│   └── notes_backup.txt
├── DocumentsBackup/
│   ├── notes.txt
│   ├── notes_backup.txt
│   └── tasks.txt
└── Scripts/
    └── todo.txt
```

The `DocumentsBackup` directory still contains the original `tasks.txt` file because it was copied in Step 4 before the file was renamed and moved.

This step demonstrates how to rename files using `mv`, move files between directories using relative paths, and verify file operations using `ls`.

These skills are useful in Linux system administration when organizing files, relocating scripts, and managing system configurations.

## **Challenges**

## **What I Learned**

## **Next Steps**
