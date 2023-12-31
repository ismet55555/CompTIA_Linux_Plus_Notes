<p align="center"><img width="150" alt="portfolio_view" src="logo.png"></p>

<h1 align="center">CompTIA Linux+ Certificate Notes</h1>

- [Users and Groups](#users-and-groups)
  - [Users: Create, Modify, and Delete](#users-create-modify-and-delete)
  - [Groups: Create, Modify, and Delete](#groups-create-modify-and-delete)
  - [Query Users and Groups](#query-users-and-groups)
  - [Account Profile](#account-profile)
- [Permissions and Ownership](#permissions-and-ownership)
  - [File and Directory Permissions](#file-and-directory-permissions)
  - [File and Directory Ownership](#file-and-directory-ownership)
  - [Special Permissions and Attributes](#special-permissions-and-attributes)
  - [Access Control Lists (ACLs)](#access-control-lists-acls)
  - [Troubleshooting Permissions Issues](#troubleshooting-permissions-issues)
- [Storage](#storage)
  - [File Systems](#file-systems)
  - [Partitioning](#partitioning)
  - [`/etc/fstab` file](#etcfstab-file)
  - [`etc/crypttab` file](#etccrypttab-file)
  - [Troubleshooting Storage Issues](#troubleshooting-storage-issues)
- [Files and Directories](#files-and-directories)
- [Kernel Modules](#kernel-modules)
- [Linux Boot Process](#linux-boot-process)
- [System Components](#system-components)
- [Devices](#devices)
- [Networking](#networking)
- [Packages and Software](#packages-and-software)
- [Securing Linux Systems](#securing-linux-systems)
  - [Cybersecurity Best Practices](#cybersecurity-best-practices)
    - [Encryption](#encryption)
    - [Hashing](#hashing)
    - [Network Configurations](#network-configurations)
    - [Best Practices](#best-practices)
  - [Identify and Access Management (IAM)](#identify-and-access-management-iam)
    - [SSH](#ssh)
    - [Pluggable Auth Modules (PAM)](#pluggable-auth-modules-pam)
    - [Public Key Infrastructure (PKI)](#public-key-infrastructure-pki)
  - [SELinux and AppArmor](#selinux-and-apparmor)
  - [Firewalls](#firewalls)
  - [Logging Services](#logging-services)
  - [Backup, Restore, and Verify Data](#backup-restore-and-verify-data)
  - [Backup, Restore, Synchronize](#backup-restore-synchronize)
  - [Compressing Files](#compressing-files)
  - [Itengrity Checking](#itengrity-checking)

## Intro

- Multiple-choice and performance-based questions
- CompTIA Linux+ Text Book?
- Choose answers that are MOST right in MOST situations
- Most questions don't need specific syntax but reaonsing (what tool? why the tool)
- [Official Exam Overview](<https://partners.comptia.org/docs/default-source/resources/comptia-linux-xk0-005-exam-objectives-(1-0)>)
- [Exam Objectives](https://partners.comptia.org/docs/default-source/resources/comptia-linux-xk0-005-exam-objectives-(1-0))
- Questions
  - Multiple Choice
  - [Performance-based](https://www.comptia.org/blog/what-is-a-performance-based-question#:~:text=Performance%2Dbased%20questions%20on%20the,hands%2Don%20experience%20more%20thoroughly.)
    - Simulations
    - Virtual environments

## Preparation

- **Course**: *Udemy - CompTIA Linux+ Complete Course & Exam - Jason Dion*
- **Practice Exams** - *Udemy - CompTIA Linux+ Practice Exams - Jason Cannon*
- **Book** - *CompTIA Linux+ Study Guide - Richard Blum, Christine Breshahan*

## Linux Installation

- Different distribution have different requirements
- Mind intended system function
- Plan appropriate partitioning strategies
- Virtual/Swap memory partition -> Swap space [2x RAM]
- Linux must at least 1 file system (ie. root: `/`)
- Multiple file system ensures recovery/backup if one file system messes up
- Hardware
  - Not all hardware work on all linux distributions
  - Hardware Compatibility List (HCL) - Database that stores hardware devices that distro supports
  - Storage drive
    - Check how many devices can be installed
    - Technology interface
    - Controller used
    - Capacity
  - CPU
    - Server desktop market
    - Clock rate
    - Cache size
    - Hyper-threading support
  - Memory
    - How much physical RAM is installed
    - DDR SDRAM Generation
  - Network Card
    - Maximum bandwidth
    - Network technology supported
  - Input Devices
    - Mouse
    - Keyboard
    - USB support
  - Monitor
    - Refresh rate range
    - Maximum pixel resolution
  - Display Adapter
    - Chipset
    - Video RAM
    - Connection Interfaces integrated into the CPU
    - Graphics card
- Boot
  - Removable Media
  - Install ISO on local drive (also with virtual machines)
  - PXE and NFS
    - Fileserver on network
    - When booted up, will grabs installation files from insatllation file server
    - Great for automatic linux installation and setup
- Installation of Linux
  - Each distro has a installation program

### Install Linux in Virtual Machine with VirtualBox

- Download and install Oracle VirtualBox for your computer architecture
  - Link: TODO
- TODO

## Linux Design Pilosophy

- **Open Source** - Freely download, modify, and redistribute
  - GNU General Public License
  - Apache
  - MIT
  - Creative Common
- Proprietry - Licensed software that has restrictions for usage
- Distros
  - Ubuntu, Debian, Fedora, Mint, Kali, etc
  - CentOS is lite version of RedHat Enterprise Linux
- Simplicity and modularity
- Linux has a steeper learning curve
- Typically not well-supported
- No definite/official version
- No official vendor-provided support
- All based on linux kernel
  - Distros add things to linux kernel

## Command Line Interface (CLI)

- Instruction flow: User -> Shell -> Linux Kernel
- **sh** - Bourne shell (Original Unix)
- **bash** - Bourne-again shell
- Typical input: Command, Options, Arguments
- Basic commands
  - `ls` - list items
  - `cd` - change directory
  - `cp` - copies fiels or directiers
  - `mkdir` - make directory
  - `clear` - clear the screen
  - `cat` - view contents of file
  - `less` - view contents of file on one screen
  - ....

### Getting Help

- `man` pages - details to CLI commands
- `apropos` - search the name of section of all man pages
- `whatis` - display a brief description of the given command
- `info` - display information page of a command (similar to man pages)

# Users and Groups

Three types of Linux user accounts:

  1. **root**

- Superuser
- Admin tasks
  - password reset,
- Provide security for some applications and commands
- More powerful than local admin on windows
- Do not log in as root user
- ID (uid) is always 0

  2. **standard**

- Regular system user
  - Runs applications
  - Configures databases
  - Creates websites
  - etc
- Should not be shared with anyone
- Exercise least privellage
  - Give users only as much access as needed to perform certain tasks

  3. **service**

- Specific to the service (ie. web server, database)
- No interactive login
- Run in background
- Often have configuration files
- Perform a single function (ie. printer service)

- Always log into system with non-privelaged user account

- Substitute/Switch User

  - `su`
    - Switch user creds
    - `su - someuser`
  - `su -root` / `sudo su` - Switches to creds to root user
  - `sudo`
    - Enables server admin to delegate commands to users without full privelages
    - User of this command must be in `/etc/sudoers` file -> `visudo` editor needed to edit
  - `sudoedit`
    - Permits a user to edit a file with own creds, even if only available to root user
    - Any member in `editors` group to edit file
    - `%editors ALL = sudoedit /path/to/file`
  - `visudo`
    - DO NOT edit `/etc/sudoers` file with standard text editors
    - This command also verifies `/etc/sudoers` syntax before committing changes
    - `-c` - Check sudoers file for errors
    - `-f` - Edit or check sudoers file in different location than default location
    - `-s` - Check sudoers file in strict mode
    - `-x` - Output sudoers file in JSON form

- "Wheel" group

  - Members exercise root priileges with less potential for damaging the system
  - Can use `sudo` command to avoid signing in as root user
  - TODO: More explanation

- Polkit (PolicyKit)

  - Controls system-wide privileges that allows non-privileged processes to
    communicate with privileged ones
  - Allows for fine-grained control
  - Uses policy files (XML) that defines what is and is not allowed
  - Used in modern Linux desktop environments (GNOME, KDE)
  - `pkexec` - Execute command with elevated privileges
    - `pkexec mkdir /Jason`
  - **NOTE**: `sudo` may be easier to use instead of `pkexec`
  - Examples:
    - TODO

## Users: Create, Modify, and Delete

- Editing user accounts

  - `useradd [options] [username]`
    - Create new user account
    - Does not set a password for user account
    - `-c` - Full name of user
    - `-e` - Account expiration date
    - `-s` - Set default shell of created user
    - `-D` - View default configurations for new user (dry run)
  - `usermod`
    - Modify user account
    - Examples:
      - Change username: `sudo usermod --login my_new_username my_current_username`
      - Change user id: `sudo usermod --uid 7 ismet`
  - `userdel`
    - Delete a user account
    - **NOTE:** Doesn't automatically delete the user directory
    - Examples:
      - Delete user: `sudo userdel <USERNAME>`
      - Delete user with their home directory: `sudo userdel -r <USERNAME>`

- `passwd`
  - Used by `root` user to set or reset password for any user
  - A user can do this themselves
  - Set password for user
    - `sudo passwd <USERNAME>`
  - Lock/unlock user password
    - `sudo passwd --lock <USERNAME>`
    - `sudo passwd --unlock <USERNAME>`

- `/etc/passwd` file
  - File storing user account info
  - Does not contain actual passwords

- `/etc/shadow` file
  - Modern storage location for hashed passwords
  - Has additional account info
    - Username
    - Hashed password
    - Days since password changed
    - Days before password must be changed
    - Days until user is warned to change password
    - Days after password expires that account gets disabled
    - Days account has been disabled
    - Unused field for future use
  - Only root has access to this

- `chage`
  - Change user account and password expiry information
  - Change expiration of password
    - `sudo chage -E 2026/12/31` (<YEAR>/<MONTH>/<DAY>)
  - Information about user password (ie. exprirations)
    - `sudo chage -l <USERNAME>`

- `/etc/login.defs` file
  - Required file that defines the site-specific configuration for the shadow password suite.
  - Stores configurations for users accounts and groups
  - Configurations include:
    - Password aging controls
    - Min and max value for UID selection
    - Default umask
    - Encryption method used to encrypt passwords

## Groups: Create, Modify, and Delete

- Groups simplify admin tasks
- Groups have a group id number (gid)
- Users can be part of more than one group

- Editing groups

  - `groupadd [options] {group names}`
    - Create a group
    - `-g` - With friendly name or id
    - `-f` - Exit with success if group already exists
    - `-o` - Allow group with non-unique group id
    - Does not create members or passwords
  - `groupmod`
    - Modify a group
    - `-g` - change group id
    - `-n` - rename group
  - `groupdel`
    - Delete a group
    - Will not delete user accounts that are members of the group
    - `gropudel [options] <GROUP NAME>`

- `/etc/group`
  - Group information for all groups
  - Each group has four pieces of info
  - Example entry: `adm:x:4:syslog,ismet`
  - `<NAME>:<PASSWORD>:<ID>:<LIST>`
    - NAME - User-friendly name of group
    - PASSWORD - Required to enter this group (`x` means password stored in `/etc/gshadow`)
    - ID - Unique ID of the group
    - LIST - User accounts that are members of group (new group has no members)

- Adding a user account to a group
  - `sudo usermod -aG <GROUPS> <USER>`
  - `-a` or `--append` - Append user to group
  - `-G` or `--groups` - List of groups (comma separated)

## Query Users and Groups

- `whoami`

  - Display the username of currently logged in user

- `who [options]`

  - Details of users currently logged in
  - `-u` - User idle time (`.` currently active user, `old` inactive for over 24 hours)
  - `am i` - Only information about user who ran the command

- `w [options] <username>`

  - Disdplay the details of users that are currently logged in to a system an their transactions
  - Output first line - Status of the system
  - Output second line - Table column list of users logged in the system
  - Output last column - Current activities of the users

- `last [options]`

  - Displays the history of user login and logout actions
  - Actual time and date
  - Retrieves info from the `/var/log/wtmp` file
  - Essentially what commands were run recently on a given system
  - `last 1` - Filter users logged into the first terminal

- `id [opstions] <username>`

  - Display user ID (uid) and group ID (gid) info
  - No options passed - Displays info about user currently logged in
  - Passing `<username>` will show the info about specific user

  - ```bash
    uid=1000(ismet) gid=1000(ismet) groups=1000(ismet),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),122(lpad
    min),134(lxd),135(sambashare),137(docker)
    ```

## Account Profile

- Allow users to customize their profile and settings
- User files eventually are within the user's home directory (ie. `/home/<USER>/`)
- Files are unique to each users
- Files starting with `.` are considered hidden files

- `.bashrc`

  - Enables customization of the user's own bash environment
  - Can specify command aliases here with `alias`
  - Create environment variable
  - Set default directories and file permissions
  - Change default command prompt

- `.bash_profile`

  - Provides the shell configuration for the initial login environment
  - Settings for all users' interactive shells
  - This file is read with first login *prior* of using the `.bashrc`
  - Effectively part of `/etc/skel`
  - System-wide settings

- `/etc/skel/` *(directory)*

  - When new user is created, content of this directory is coppies into
    user's default home directory
  - Any files added after user creation to `/etc/skel` will not be copied over

- `/etc/profile`

  - Provides system-wide **environment variables** that are used to apply
    certain settings to user accounts
  - Only run at login

- `/etc/profile.d` *(directory)*

  - Storage location for scripts that admins may use to set
    additional system-wide variables
  - Set environment variables via scripts contained in this directory
    rather than editing `/etc/profile` directly for better control

- `/etc/bashrc`
  - System-wide configuration changes specific to bash settings
  - Bash settings for command-line environment
  - May also be `/etc/bash.bashrc`

# Permissions and Ownership

## File and Directory Permissions

- Permission

  - Access rights assigned to users that enable them to access
    or modify files and directories
  - Can be set at different levels and contexts
  - Who is allowed and restricted to access objects
  - Least privellage - Ony access what they need to access and nothing more

- `ls -l`

  - See all files and directories with their access permissions

  - ```bash
    drwxrwxr-x 2 ismet ismet    4096  Nov 20 20:19 .
    drwxrwxr-x 3 ismet ismet    4096  Nov 13 09:46 ..
    -rw-rw-r-- 1 ismet learners 11324 Nov 20 20:25 NOTES.md
    -rw-rw-r-- 1 root  hackers  1135  Nov 21 17:25 important.blah
    ```

  - Column 1 - Permission attribute string (ie. `-rw-rw-r--`)
  - Column 2 - Number of links to that file/directory
    - For directories it's number of sub-directories plus 2 (`.` and `..`)
    - Links are similar to shortcuts in windows
  - Column 3 - User Owner (ie. `ismet`)
  - Column 4 - Group granted access by admin (ie. `hackers`)
  - Column 5 - Size in bytes
  - Column 6 - Datetime file was created or modified
  - Column 7 - Name of file/directory

- **Permission Attributes**

  - Define what user are allowed to do in a particular file or directory
  - Depends if file or directory
  - Files
    - `r` - read - Access and view content
    - `w` - write - Ability to save changes / write to file
    - `x` - execute - Run script/program/software
  - Directories
    - `r` - read - List directory content
    - `w` - write - Create, rename, delete files
    - `x` - execute - Access directory and execute file from that directory or perform task

- **Permission Contexts**

  - Permission attributes apply to one of three contexts
  - `u` - owner - Owner of file or directory (a user). Can only do things that effect themselves
  - `g` - group - File or directory group. All users that belong to group have permissions
  - `o` - other - All other users. Not the owner and not the group member

- **Permission String**

  - Examples:
    - For File: `-rw-rw-r--`
    - For Directory: `drwxrwxr-x`
  - 11 characters long
    1. Type of file
       - `d` - directory
       - `-` - file
    2. Owner Permission - read (r)
    3. Owner Permission - write (w)
    4. Owner Permission - execute (x)
    5. Group Permission - read (r)
    6. Group Permission - write (w)
    7. Group Permission - execute (x)
    8. Other Permission - read (r)
    9. Other Permission - write (w)
    10. Other Permission - execute (x)
    11. Access method for the file
        - `.` - SELinux security context
        - `+` - Alternative access methods

- **Changing Permissions**

  - `chmod [options] {mode} {file/directory name}`
  - Enables the item owner or system admin (root) to modify the permissions of a file or directory
  - `-c` - Report changes
  - `-f` - Hide error messages
  - `-v` - Display diagnostic entry
  - `-R` - Recursively modify permissions
  - Supports two different modes:
    1. **Symbolic**
    2. **Absolute**
  - **chmod: Symbolic Mode**
    - `chmod {context}{operators}{attributes} {file/dir names}`
    - Example:
      - `chmod u+rw my_dir` - Give user rights to read and write
      - `chmod g-x my_file` - Remove exeuteable rights from group
    - Context - `u/g/o/a` - user/group/other/all ("who is affected")
    - Operators - `+/-/=` - grant/deny/exactly assign
    - Attributes - `r/w/x` - read/write/execute ("what can they do")
  - **chomd: Absolute Mode**
    - `chmod {number} {file/dir names}`
    - Uses octal (base-8) numbers to specify permissions
    - Each permission has a number associated with it, add up to get permission
      - `4` - read
      - `2` - write
      - `1` - Execute
    - Example:
      - `7` -> `421` -> read, write, execute
      - `6` -> `42` -> read, write
    - Complete final permission is a three-digit number that corresponds to
      the owner, group, and others (ie, `774`)
      - First digit: user
      - Second digit: group
      - Third digit: other
    - Example: `752`
      - `7` - user - read, write, execute
      - `5` - group - read, execute
      - `2` - othes - write

- `umask`
  - Used to set the default permissions for newly created files and directories
  - Manage read/write/execute permissions that are masked out (restricted) for
    newly created files by the user
  - Default Permissions: By default, Linux sets permissions for new files to
    666 (read and write for everyone) and for directories to
    777 (read, write, and execute for everyone).
  - `umask` acts like a filter. It subtracts permissions from the default set.
    So, if you set a umask of 022, it removes write permissions for the group
    and others. This means new files will have 644 (read and write for the
    owner, read-only for group and others) and directories will have
    755 (read, write, and execute for the owner, read and execute for group
    and others).
  - Can be set in `.bashrc` or `.bash_profile`
  - `umask -S` - Display symbolic value
  - `umask [mask]` - Setting umask for file and dir
  - Difference between `chmod` and `umask`
    - `umask` changes *default* permissions for *newly* created files and directories
    - `chmod` sets permissions on files and directories that *already exist*
  - Examples:
    - `umask a+r` - Take away read for all
    - `umask 020` - Take away write from group
    - `umask 077` - Take away read, write, and execute from group and other

## File and Directory Ownership

- Ownership
  - Property by which a user can apply and modify the permissions
    of a file or directory
- Only the superuser (root user) can change the permissions of an object
  owned by others
- Every file is owned by specific user and specific group

- **Changing Ownership**
  - `chown`
    - Change the owner and/or the group of a file or directory
    - `chown {username}:{group name} {file/directory name}`
    - `chown {username}:{group} {file/directory name}` - Change user and group owner
    - `chown {username} {file/directory name}` - Change user owner
    - `chown :{group name} {file/directory name}` - change group only
    - `chown {username}: {file/directory name}` - Change user owner and assign to user owner login group
    - `-R` - Recuirsively change ownership throughout directory structure

  - `chgrp`
    - Change group ownership of a file or directory
    - `chgrp {group name} {file/directory name}`

## Special Permissions and Attributes

- Special permission - Less privileged users are allowed to execute a file
  by assuming the privileges of the file's owner or group

- Set user ID (SUID)
  - User is allowed to have similar permissions as the
    owner of the file
  - When a file has the setuid bit set, any user who runs that file will
    have the file executed with the permissions of the file's owner, not
    the user who ran the file.
- Set group ID (SGID)
  - User is allowed to have similar permissions as the
    group owner of the files and directories

- `ls -la` - Determining SUID/SGID
- Files can have one or more *attributes* set that define how the system
  interacts with them

- Can use `chmod` in symbolic (+s) or absolute mode
  - SUID Symbolic: `chmod u+s {filename}`  (Use `-` to remove)
  - SUID Absolute: `chmod 4### {filename}`  (Use `0###` to remove)
  - SGID Symbolic: `chmod g+s {directory name}`
  - SGID Absolute: `chmod 2### {directory name}`

- **Sticky Bit** (`+t`)
  - Special permission bit that protects files in a directory
  - Must be applied to the directory
  - Users may be able to write and execute, but can't delete items
  - Symbolic: `chmod +t {directory name}`
  - Absolute: `chmod 1### {directory name}`

- **Immutable Flag (`+i`)**
  - Attribute of a file or directory that prevents it from being modified
    (even by the root user)
  - Useful for fiels that are highly sensitive and important
  - File:
    - Set: `chattr +i /path/to/file`
    - Unset: `chattr -i /path/to/file`
  - Directory:
    - Set: `chattr +i -R /path/to/directory`
    - Unset: `chattr -i -R /path/to/directory`

  - `lsattr`
    - List the attributes of a file or directory
    - `lsattr [options] {file or directory name}`
    - `-R` - Recuirsively list attributes of items
    - `-a` - List all files
    - `-d` - List directories
    - `-v` - List file's version number

  - `chattr`
    - Used to change the attributes of a file or directory
    - `chattr [-R] [-v {version}] [+-{attributes}] {file or directory name}`
    - `-R` - Recursively change attributes
    - `-v` - Set file version number
    - `+I` - Mark file as read-only and immutable
    - `-I` - Remove read-only

## Access Control Lists (ACLs)

- Enable a more granular level of control than simply using file permissions
- Can set access to multiple groups on one directory

- `getfacl`
  - Useful when retrieveing the ACLs of files and directories
  - Will show any permission attributes with object

- `setfacl`
  - Change the permissions associated with the ACL of a file or directory
  - `setfacl [-bR] [-mx {acl_spec}] {file/directory name}`
  - `-r` - Recuirsively set ACL options
  - `-S` - Set ACL
  - `-m` - Modify existing ACL
  - `-x` - Remove entries from existing ACL
  - `-b` - Remove all entries except standard permissions
  - acl_spec
    - Users: u:{username}: {permissions}
    - Group: g:{group name}: {permissions}
  - Example:
    - `sudo setfacl -R -m g:My-Group:r /My-Dir`

## Troubleshooting Permissions Issues

- CompTIA Troubleshooting steps
  1. Identify the problem
  2. Establish theory of probable cause
  3. Test the theory to determine the cause
  4. Establish an action plan
  5. Implement the solution
  6. Verify full system functionality
  7. Document findings, actions, and outcomes

- `ls -la` - Check permissions and ownership
- `groups {username}` - Check user's group membership
- `usermod` - Change group membership
- `lid`, `liduser-lid`
  - Retrieve all members of a group
- `getent`
  - Retrieve group members (or services) of non-standard authentication methods
  - `getent group`, `getent services`

- Critical steps
  1. Follow troubleshooting strategy
  2. Verify permissions and ownership (ie. `ls -la`)
  3. Verify special permissions are set properly (ie. sticky bits, immutable flags)
  4. Ensure proper owner and owning group set

# Storage

## File Systems

- Types of storage devices
  - Block Devices - Read/Write in blocks of data (e.g., hard drives, solid-state devices)
  - Character Devices - Read/Write character streams of data (e.g., keyboards, mice, serial ports)
- File System
  - Data structure used by an operating system to store, retrieve, organize, and manage files
      and directories on storage devices
  - Supported Linux file systems
    - `FAT` - File allocation Table - Older file system, used for compatibility
    - `ext2` - Used to be native linux file system on older releases
    - `ext3` - Faster in recovering data and better ensures data integrity of abrupt system shutdowns
    - `ext4` - Supports volumes up to 1 exabyte and files up to 16 terabytes in size
    - `XFS` - 64-bit, high-performance journaling file system that provides fast recovery and can handle large files efficiently
    - `BTRFS` - Modern filesystem. Supports volumes up to 16 exabytes in size and up to 18 quintillion files on each volume
  - File system protocols
    - Server Message Block (SMB)
      - Allows users to have access to files over the local network
      - Server-client architecture
      - Better for mixture of windows and linux filesystems
      - Microsoft Windows supports SMB by default
    - Common Internet File system (CIFS)
      - Some linux distribution refer to SMB as CIFS
      - Version of SMB, rarely in use today, replaced by later versions
    - Network File System (NFS)
      - Better for all linux networks and filesystems
      - Not supported by Microsoft Windows by default
  - Index Node (Inode)
    - Stores metadata about a file or directory on a file system
    - Can included time-based values (created, modified, etc), permission and ownership info,
    - Determine filesystem ionodes:
      - `df -i <PATH>`
  - Virtual File System (VFS)
    - Filesystem created as interface between kernel and real file system
    - Translates real file system details to kernel
    - Can mount many file systems on OS, and will appear uniform to system and applications
    - File system labels are used for easy identification and many be up to 16 characters long
    - Labels can be displayed or changed using the following commands
      - `e2label` - ext-based file system
      - `xfs_admin` - XFS-based file system

## Partitioning

- Partition - A section of the storage drive that logically acts as a separate drive

- 3 Types of partitions
    1. Primary
        - Contains one file system or logical drive and is sometimes referred to as a volume
        - Examples:
            - swap file system - Used as buffer for actual physical memory
            - boot partition
    2. Extended
        - Contains several file systems, which are referred to as logical drives
        - Does not contain data
        - Has separate partition table
    3. Logical
        - Partitioned and allocated as an independent unit and functions as a separate drive

- Modifying partitions
  - `fdisk`
    - Used to create, modify, or delete partitions on a storage drive
    - `-b` - Number of drive sectors
    - `-H` - Number of drive heads
    - `-S` - Number of sectors per track
    - `-s` - Print partition size in blocks
    - `-l` - List partition tables for devices
    - Within the `fdisk` menu:
      - `n` - Create new partitions
      - `d` - Remove partition
      - `p` - List exixsting partitions
      - `w` - Write drive changes and exit utility
      - `q` - Cancel changes made and exit utility
  - `partprobe`
    - Update the kernel with changes that now exist within the partition table
    - If there are any changes, kernel is updated with those changes
    - Used after using `fdisk` or `parted`
    - Examples:
      - Update all: `partprobe`
      - Update added new partition: `partprobe /dev/sdb`
      - Only do dry run: `partprobe --dry-run`
  - `mkfs`
    - Build a Linux file system on a device, which is usually a drive partition
    - Typically used like this: `mkfs.<FILE_SYSTEM_TYPE>`
      - Examples: `mkfs.xfs /dev/sdb`, `mkfs.ext4 /dev/sdb2`
      -
    - `-v` - Produce verbose output - Program process
    - `-V` - Produce verbose output - All file system-specific commands executed
    - `-t {fs type}` - Specify type of file system to build
    - `fs -options` - Pass system-specific options to the file system builder
    - `-c` - Check the device for bad blocks before building the file system
    - `-l {filename}` - Read the list of bad blocks from a specific file
    - Can run it two ways
            1. `mkfs [options] {device name}`
            2. `mkfs {file system type} [options] {device name}`
  - `parted`
    - Partition manipulation program
    - Create, destroy, and resize partitions
    - Runs GNU parted utility
    - Can use interactive mode (ie. `sudo parted`)
      - `select` - choose device or partition to modify
      - `mkpart` - Create partition with file system type specified
      - `print` - List partition table
      - `resizepart` - Resize and modify a partition's end position
      - `rm` - Delete partition
      - `quit` - Quite interactive mode
    - Example:
      - Open interactive mode: `parted /dev/sdb`
      - `mkpart` -> Enter partition items

## `/etc/fstab` file

- "File system table"
- Stores info about storage devices and partitions and where and how they should be mounted
- Config file that controls how file systems are treated when they are introduced to a system
- Read by system during boot up process
- Only edited by `root` user
- Each line in this file has 6 fields:

  - ```
      <file system> <mount point> <type> <options> <dump> <pass>
      ```

  - File system - Name of the device (UUID) or file system to mount (`/mnt/something`)
  - Mount Point - Where to mount file system (ie. `/home`)
  - File system type - Type of file system (ie. `ext4`, `swap`) (Partition ID: 82)
  - Options - Comma-seperated options that will be activated when the file system is mounted
  - Dump - If the dump utility should back up file system (0 or 1)
  - Pass - fsck options. Order in which `fsck` utility should check file system

## `etc/crypttab` file

- Information about encrypted devices and partitions that must be unlocked and mounted
  on system boot
- Encrypted block devices that are set up during system boot

- ```
  <volume-name> <encrypted-device> <key-file> <options>
  ```

## Overall process for setting up storage on linux machines

1. Partition storage device (ie. `fdisk`, `parted`)
2. Format partition with a file system (ie. `mkfs`)
3. Add formatted partition to `/etc/fstab` file

## `/dev` directory

- Special file that contains details about all the files and subdirectories housed within it
- Everything in linux is treated as a file, even file systems

## Storage Device Naming

- `/dev/sda1` - Controller-based naming
  - `sd` - Type of controller
  - `a` - First whole physical drive (`a`, `b`, etc)
  - `1` - First partition on drive (`1`, `2`, etc)
- `/dev/disk/by-id/<DEVICE_ID>`
  - Device's hardware serial number
  - Examples:
    - `/dev/disk/by-id/nvme-eui.6479a765c13012c5-part1`
    - `/dev/disk/by-id/nvme-ESE2A047-M24_NVMe_Phison_1024GB_1782073611ED00110458-part8`
- `/dev/disk/by-path/<PHYSICAL PATH`
  - Shortest physical path to the device
  - Example:
    - `/dev/disk/by-path/pci-0000:00:0e.0-pci-10000:e1:00.0-nvme-1-part1`
- `/dev/disk/by-uuid/<DEVICE UUID>`
  - Universally unique identifier (UUID)
  - Example:
    - `/dev/disk/by-uuid/5cb09b2f-53d2-4f43-a292-8ebe4d65371g`
- Other naming:
  - `/dev/disk/by-label/<DEVICE_LABEL>`

## Special character devices in `/dev`

- `/dev/null`
  - Virtual device that discards anything you send or redirect into it
  - Ie. a big black hole for data
  - Example usage:
    - Discard output: `echo "hello" > /dev/null`
    - Suppress errors: `touch file 2> /dev/null`
- `/dev/zero`
  - Returns a null character anytime you read from it
  - Send back the ASCII null character of 0x00
  - Example usage:
    - Sanitize hard drive: `dd if=/dev/zero of=/dev/sda1 bs=1GB count=1024`
- `/dev/urandom`
  - Returns a randomized series of pseudorandom numbers
  - Example usage:
    - Get 5 random characters: `head -c 5 /dev/urandom`
    - Generate secure token: `dd if=/dev/urandom  count=1 bs=128 | sha512sum`

## RAID (Redundant Array of Independent or Inexpensive Disks)

- Way of storing the same data in different places on multiple physical disks
  to protect data in the case of a drive failure.
- RAID arrays appear to the OS as a single logical drive
- Techniques used in RAID:
    1. Striping
        - Combines multiple smaller physical disks to logical act as a single largert disk
        - Used to combine physical storage into one single logical storage
    2. Mirroring
        - Combines two physical hard drives into a single logical volume where an
          identical copy of everything is put on both drives
    3. Parity
        - Used for fault tolerance by calculating the data in two drives and storing
          the results on a different drive
        - Storing information used to reconstruct the data
        - If you know the value of any two of the three items, you can calculate the third
- RAID is classified with levels (ie. 0, 1, ..., 10):
  - <https://en.wikipedia.org/wiki/Standard_RAID_levels>
  - RAID 0
    - Striping
    - Each drive holds half of the data
    - Speed boost
    - No loss of disk space
    - BUT no data redundancy!
  - RAID 1
    - Mirroring
    - Disks have same data
    - Data redundancy
    - BUT loss of space!
  - RAID 5 *(Most popular)*
    - Striping and Parity
    - Data redundancy and pairty
    - Need at least 3 disks (need at least 2 disks to compute the parity on the other disk)
    - Can lose 1 drive and still calculate based on remaining 2
    - More efficient to create RAID 5, in terms of space, than RAID 1 using a
          mirrored array
  - RAID 6
    - Striping and DUAL Parity
    - Need at least 4 disks
    - Can lose 2 drives and still calculate based on remaining 2
  - RAID 10
    - Mirroring and Striping
    - "RAID of RAIDS"
    - Need at least 4 disks
    - Drives come in disk pairs to be stripped, then the stripped
          disk pair is mirrored to another disk pair
    - Benefit of RAID 0 and RAID 1
    - Losing half of disk space

- `/proc/mdstat` file
  - Contains a snapshot of the kernel's RAID/md state
  - Shows what RAID levels can be supported by kernel
  - Shows active RAID arrays with participating disk drives
  - Shows disk status (ie. `[UUU_]` -> Up Up Up Down)

## Logical Volume Manager (LVM)

- Device Mapper - Creates virtual device and passes data from that virtual device
to one or more physical devices.

- DM-Multipath - Linux kernel feature that rrovides redundancy and improved
performance for block storage devices.
  - If one path fails, it will switch to other remaining paths

- `mdadm`
  - Tool used to create and manage software- based RAID arrays
  - Create manage and monitor RAID arrays
  - Data is in multiple different storage devices
  - Alternative to using device mapper and DM-Multipath

- LVM maps whole *physical devices* and partitions into one or more virtual containers
  called *volume groups*

- Within *volume groups* there are one or more *logical volumes* that the system/user/apps
  interact with

- Can dynamically create, delete, and resize volumes without system reboot

- Can map logical volumes across multiple physical devices

- Create virtual snapshots of each logical volume

- `/dev/mapper`
  - Shows all logical volumes on given system managed by LVM
  - Typically named: `/dev/mapper/<VOLUME_GROUP_NAME>-<LOGICAL_VOLUME_NAME>`

- Tools for LVM ([Documentation](https://linux.die.net/man/8/lvm))
    **NOTE:** Exam will not ask for each and every one of these commands
    1. Physical volume tools
        - `pvscan` - Scan for all physical devices being used as physical volume
        - `pvcreate`  - Initialize a drive or parittion to use as a phsycial volume
        - `pvdisplay` - Lists attributes of physical volumes
        - `pvchange` - Changes attributes of a physical volume
        - `pvs` - Displays info about physical volumes
        - `pvck` - Check metadata of physical volumes
        - `pvremove` - Removes physical volumes
    2. Volume group tools
        - `vgscan` - Scan for all phsycial devices for volume groups
        - ...
    3. Logical volume tools
        - ...

### Typical LVM Step Process

1. Connect/Create physical disk
2. Partition the drive
3. Add the new physical volume `pvcreate`
4. Create new volume group **OR** add physical volume to existing volume group
5. Create a new logical volume **OR** Extend existing logical volume to unused physical volume

Example:

- Create physical volume
  - `pvcreate /dev/sdb1`
- Show details
  - `pvscan`
  - `pvdisplay`
- Create a new "backup" volume group using the physical volume
  - `vgcreate backup /dev/sdb1`
- Show details
  - `vgscan`
  - `vgdisplay`
- Create two logical volumes in "backup" volume group
  - `lvcreate --name sys_backup --size 2GB backup`
  - `lvcreate --name data_backup --size 2GB backup`
- Show details
  - `lvscan`
  - `lvdisplay`
- Extend one logical volume by 3GB
  - `lvextend --size +3GB /dev/backup/data_backup`
- Create filesystems on new logical volumes:
  - `mkfs.xfs /dev/backup/sys_backup`
  - `mkfs.ext4 /dev/backup/data_backup`

## Mounting File Systems

- Mounting file system makes it available for users
- Mount Point
  - Access point that is typically an empty directory wher ea file system is loaded
      or mounted to make it accessible to users
  - `/dev/sda`
    - `/dev/sda1` mounted on `/`
    - `/dev/sda3` mounted on `/home`
    - `/dev/sda5` mounted on `/var`

- `mount`
  - Command that loads a file system to a specified directory to make it
      accessible to users and applications
  - `mount [options] {device name} {mount point}`
  - Options:
    - `auto` - Device must be mounted automatically
    - `noauto` - Device should not be mounted automatically
    - `nouser` - Only the boot user can mount a device or a file system
    - `user` - All users can mount a device or a file filesystem
    - `exec` - Allow binaries/executables in the file system to be executed
    - `noexec` - Prevent binaries in a file system from being executed
    - `ro` - Mount file system as read only
    - `rw` - Mount file system as read or write
    - `sync` - Input and output operations should be done synchronously
    - `async` - Input and output operations should be done asynchronously

- `umount`
  - Disassociate a mounted file system from the directory
  - File system cannot be in use (any files open)
  - `umount [options] {mount point}`
  - Options:
    - `-f` - Force unmount a file system
    - `-l` - Lazy unmounting. References to file system cleaned up once file system is not in use
    - `-R` - Recuirsively unmounts mount points (ie. `/dev`)
    - `-t {type}` - Only unmount specific file system types (ie. `ext4`)
    - `-O` - Unmount file systems in `/etc/fstab`
    - `-fake` - Test the unmounting procedure (dry run)

- Example usage:
  - Make a directory to mount file system to
    - `sudo mkdir -p /backup/sys`
  - Mount logical volume
    - `sudo mount /dev/backup/sys_backup /backup/sys`
  - Show mounted file systems
    - `mount`
  - Unmount
    - `sudo umount /dev/backup`
  - Ensure mounting on system boot
    - Edit: `sudo vim /etc/fstab`
    - Add: `/dev/backup/sys_backup /backup/sys xfs defaults 0 0`
    - Save and exit VIM with :x
    - Test mount fstab: `sudo mount -a`

- Other mounting options
  - `systemd.mount`
    - Can be used to create a new mount unit to mount the file system
    - Add unit to `/etc/systemd/system/`
    - Example: `/etc/systemd/system/var-lib-docker.mount`
    - Then: `systemctl enable var-lib-docker.mount`

  - Filesystem in USERspace (FUSE)
    - Lets non-privileged users create own file system without editing the underlying
          kernel code
    - Can be used for local interaction of cloud-based storage

## Managing File Systems

- `/etc/mtab` file
  - Reports the status of currently mounted file systems
  - `/proc/mounts` - More accurate and includes more up-to-date file system info

- `/proc/partitions` file
  - Contains info about each partition attached to the system
  - Example contents:

        ```txt
        major minor  #blocks  name
         259        0 1000204632 nvme0n1
         259        1     245760 nvme0n1p1
         259        2     131072 nvme0n1p2
         259        3  585253888 nvme0n1p3
        ```

- `lsblk`
  - Display info about block storage devices available on the system
  - `lsblk -a` example output:

        ```txt
        NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
        sda            8:0    1     0B  0 disk 
        sdb            8:16   1     0B  0 disk 
        nvme0n1      259:0    0 953.9G  0 disk 
        ├─nvme0n1p1  259:1    0   240M  0 part /boot/efi
        ├─nvme0n1p2  259:2    0   128M  0 part 
        ├─nvme0n1p3  259:3    0 558.1G  0 part 
        ├─nvme0n1p4  259:4    0     1G  0 part 
        ├─nvme0n1p5  259:5    0  16.9G  0 part 
        ├─nvme0n1p6  259:6    0   1.5G  0 part 
        ├─nvme0n1p7  259:7    0   954M  0 part 
        ├─nvme0n1p8  259:8    0   954M  0 part 
        ├─nvme0n1p9  259:9    0  44.7G  0 part /var/snap/firefox/common/host-hunspell
        │                                      /
        ├─nvme0n1p10 259:10   0  72.6G  0 part /var
        ├─nvme0n1p11 259:11   0  22.4G  0 part [SWAP]
        └─nvme0n1p12 259:12   0 234.5G  0 part /home
        ```

- `blkid`
  - Prints each block device in a float format and includes some additional info
  - `blkid -o list` example output:

  - ```txt

    device                    fs_type    label       mount point                   UUID
        --------------------------------------------------------------------------------------------------------------------
    
        /dev/nvme0n1p11           swap                   [SWAP]                        eec1832c-616d-45ed-a66b-e788e6bf8326
        /dev/nvme0n1p9            ext4                   /                             3cb09b2f-53d2-4f43-a292-8ebe4d65371a
        /dev/nvme0n1p7                                   (not mounted)
        /dev/nvme0n1p5                                   (not mounted)
        /dev/nvme0n1p3                                   (not mounted)
        /dev/nvme0n1p1                                   /boot/efi
        /dev/nvme0n1p12                                  /home
        /dev/nvme0n1p8                                   (not mounted)
        /dev/nvme0n1p10                                  /var
        /dev/nvme0n1p6                                   (not mounted)
        /dev/nvme0n1p4                                   (not mounted)
        /dev/nvme0n1p2                                   (not mounted)
    ```

- `fsck`
  - Check for correctness and validity of a file system
  - Repair file system: `fsck -r {device/file system name}`

- `resize2fs`
  - Increase or decreate file system size
  - Typically used after resizing logical volumes in LVM
  - Resize ext2, ext3, or ext4 file system
  - `resize2fs [options] {device/file system name} [desired size]`
  - If no size is specified, fill up remaining open space on volume

- `tune2fs`
  - Adjust various tunable parameters of that ext2/ext3 file systems
  - Can use to add jounral to an existing ext2 and ext3 file system
  - `tune2fs [options] {device/file system name}`

- `dumpe2fs`
  - Prints the superblock and block group info for the selected device
  - "Superblock" - Contains metadata about the file system (size, type, status)
  - For ext2, ext3, or ext4 file system
  - Can be used for faulty file system

- XFS File System Tools
  - `xfs_info` - Display details about the XFS file system
  - `xfs_admin` - Change the parameters of an XFS file system
  - `xfs_metadump` - Copy the superblock metadata of the XFS file system to a file
  - `xfs_growfs` - Expand the XFS file system
  - `xfs_copy` - Copy the contents of the XFS file system to another location
  - `xfs_repair`
  - `xfs_db`

- `lsscsi`
  - List info about SCSI (SKUH-zee) devices connected to a linux system
  - SCSI (Small Computer System Interface) is used to connect and communicate between
      computers and peripheral devices, such as hard disk devices, tape drives, CD/DVD,
      printers, and scanners.
  - Relatively old devices

- `fcstat`
  - Interacts with and displays statistics of fibre channels connected devices

## Linux Directory Structure

- Filesystem Hierarchy Standard (FHS) specifies a set of guidelines for the names
  of files and directories and their locations on Linux systems

- `/` - Top-most directory in linux system

```txt
/
├── bin -> usr/bin        - Essential command-line utilities and binaries (ie. `ls`)
├── boot                  - Files necessary to boot Linux OS
├── cdrom
├── dev                   - Hardware and software device drivers (ie, hard drive, printer)
├── etc                   - Basic configuration files
├── home                  - Users' home directories, including personal files (ie. /home/ismet/)
├── lib -> usr/lib        - Shared program libraries required by kernel, CLI utils, and binaries
├── media                 - Mount points for removable media (ie CD, floppy disks)
├── mnt                   - Mount point for temporary mounting file systems (ie. USB drive)
├── opt                   - Optional files for large software packages
├── proc                  - Continually updated kernel info to user in file format (ie. `/proc/mounts`)
├── root                  - Home directory of root user
├── run
├── sbin -> usr/sbin      - Binaries used for completing the booting process which are also used by root user (ie `/sbin/ifconfig`)
├── snap
├── squashfs-root
├── srv
├── sys                   - Info about devices
├── tmp                   - Temporary files lost/cleared on system shutdown
├── usr                   - Read-only directory storing small programs and files accessible to all users
    ├── bin               - Binaries executed by all users
    ├── lib               - Libraries for executable programs
    ├── lib64             - Libraries for 64-bit systems
    ├── local            - Custom build application stored here
    ├── share            - Read-only files about the system
    ├── sbin
    ....
└── var                   - Variable files, or files that are expected to constantly change (ie. /var/log/syslog). Can include spool files.
```

## Troubleshooting Storage Issues

- `ulimit`
  - Limits the system resources for a user in a Linux-based server
  - Set 500 maximum open files for user: `ulimit -n 500`
  - Show all current limits: `ulimit -a`

- `df`
  - Displays the device's storage space
  - Ued, available, Used %, mount point

- `du`
  - Display how a device is used
  - Size of directory tree and files within it
  - Able to show how used storage is distributed

- `/sys/block/<DEVICE>/queue/scheduler`
  - Set the scheduler to use on a particular device
  - Example setting NOOP scheduler for `sda`
    - `echo noop > /sys/block/sda/queue/scheduler`

- `iostat`
  - Generates reports on CPU and device/partition usage
  - Incremental reports every 2 seconds: `iostat 2`

- `ioping`
  - Monitor I/O latency in real time
  - Troubleshoot latency with storage devices
  - Generates a report of device I/O latency in real time
  - Disk seek rate: `ioping -R /dev/sda`
  - Disk sequential speed: `ioping -RL /dev/sda`
  - Current directory: `ioping .`

- `repquota`
  - Summary of existing file quotas for a file system
  - `repquota /backup/data`

# Files and Directories

TODO

# Kernel Modules

TODO

# Linux Boot Process

TODO

# System Components

TODO

# Devices

TODO

# Networking

TODO

# Packages and Software

TODO

# Securing Linux Systems

## Cybersecurity Best Practices

- Cybersecurity
  - Protection of computer systems and digital info resources from
unauthorized access, attack, theft, or data damage.

- Confidentiality
  - Prevent data theft, no unauthorized access
  - Use encryption and access controls

- Integrity
  - Keep info/data without unauthorized modifications
  - Prevent defacement
  - Use hashing, digital signatures, certificates, change control

- Availability
  - Authorized users can access data when they need to
  - Prevent deniel of Service (DoS)
  - Use redundancy, fault tolerance, patching

- Remote Authentication Dial-In User Service (RADIUS)
  - Internet standard protocol that provides authentication, authorization, and
      accounting (AAA) services
  - Terminal Access Control Access-Control System (TACACS) - Provides AAA services for remote users

- Lightweight Directory Access Protocol (LDAP)
  - TCP/IP-based directory service protocol
  - Authenticate to LDAP service
  - Service has schema of what client can and can't do

- Kerberos
  - Auth service based on time-sensitive ticket-granting system
  - Windows-native
  - Linux has kerberos usage as well

- Chroot Jail
  - Isolate a process and its children from the rest of the system
  - Only use on processes not run as root. Root user can break out of jail.

### Encryption

- Full Drive/Disk Encryption (FDE) - Encryptes a storage drive, partition, or volume using hardware/software utilities
- File Encryption - Encrypts indiviaul files and folders
- Linux Unified Key Setup (LUKS)
  - Used to encrypt storage devices in Linux system
  - Standardizes the format of encrypted devices
  - `cryptsetup`
    - Front-end to LUKS and dm-crypt
    - `cryptsetup [options] {action} [action arguments]`
    - `isLuks` - id if a device is a LUKS device
    - `luksOpen` - Open LUKS storage device
    - `luksAddKey` - New key with a LUKS device
- `shred`
  - Securetly wipe a storage
  - Write all zeros/random data on it
- Example step process:
  - Unmount filesystem from mount point
    - `sudo umount /backup/data`
  - Clean partition
    - `sudo shred -v iterations=1 /dev/backup/data_backup`
  - Encrypt with passphrase
    - `sudo cryptsetup -v luksFormat /dev/backup/data_backup`
    - Enter passphrase
  - Let system map
    - `sudo cryptsetup luksOpoen /dev/backup/data_backup data_backup`
    - Enter passphrase
  - Verify/Search for new item
    - `ls -la /dev/mapper | grep data_backup`
  - Make a filesystem for it
    - `sudo mkfs.ext4 /dev/mapper/data_backup`
  - Mount the filesystem to location
    - `sudo mount /dev/mapper/data_backup /backup/data/`
  - Add to fstab file
    - `/dev/mapper/data_backup /backup/data ext4 nofail 0 0`

### Hashing

- Transforms plaintext input into an indecipherable, fixed-length output
- Involves a hash function that converts input in fixed-size string of bytes
- Input varies but hashlength always fixed
- Examples:
  - Password storage
    - Store hash of password
    - Modern systems add "salt" (random value unique to each user) to password before hashing
  - Data integrity
    - Hash files and verify integrity of hashed filed to make sure it did not change
    - Tools like `md5sum` or `sha256sum`
    - Packaging tools like `apt` use hashing
  - Secure data transmission
  - Network security
  - File identification

### Network Configurations

- Enable SSL/TLS
  - Encrypt data during transit
- Enable SSH
  - Disable root access
  - Enable allow list
  - Change port (ie. 2222)

### Best Practices

- Protect boot loader configuration with a password
- Enable password protection in system's BIOS/UEFI
- Can prevent kernel modules to load at boot
  - Blocklist file in `/etc/modprobe.d/
- Ensure user IDs are not being shared
- Establish a public key infrastructure for authentication
- Restrict access to cron job scheduler
- Disable the use of Ctrl-Alt-Delete to prevent users to reboot system
- Enable the `auditd` service
- Add banner when user logs into system with `/etc/issue`
- Separate OS and other data in different partitions
- Disable or uninstall unused or insecure services

## Identify and Access Management (IAM)

- IAM - Security process that provides identity, authentication, authorization mechnaisms

- Public Key Authentication
  - Used for interactive and automated connections
  - Between servers or users and servers
  - Stronger than regular password
  - Passwordless logins

### SSH

- Supports many authentication methods

- `~/.ssh/` directory
  - Contains files related to SSH keys

- Configuration files within `~/.ssh/` directory
  - `~/.ssh/id_rsa` - User's private key
  - `~/.ssh/id_rsa.pub` - User's public key
  - `~/.ssh/authorized_keys` - Public keys that SSH server accepts
  - `~/.ssh/known_hosts` - Public keys that the SSH client accepts
  - `~/.ssh/config` - SSH connection settings

- `/etc/ssh/sshd_config` file
  - Configure the SSH server
  - Edit: `vim /etc/ssh/sshd_config`
  - Settings in this file include:
    - `PasswordAuthentication` - Enable/Disable password-based SSH authentication
    - `PubkeyAuthentication` - Enable/Disable public key-based authentication
    - `Hostkey` - Location of the server's private keys
    - `UsePAM` - Enable/Disable support for Pluggable Auth Modules (PAM)
    - `Port` - Change port number for the SSH service
    - `AllowUsers`/`AllowGroups` - Allow user/group-specific access for SSH
    - `DenyUsers`/`DenyGroups` - Deny user/group-specific access for SSH
    - `PermitRootLogin` - Enable/Disable root user to log in over SSH
  - After changing: `systemctl restart sshd`

- `/etc/hosts.allow` / `/etc/hosts.deny` files
  - Allow and deny remote hosts access

- `ssh-keygen` - Generate a public/private key pair
- `ssh-copy-id` - Put user's public key (ie. `id_rsa.pub`) into remote server's `authorized_keys` file
- `ssh-add` - Add user's private keys to the running SSH key agent

### Pluggable Auth Modules (PAM)

- Help apps make proper use of user accounts in Linux
- LDAP most common use cases that uses this

- `/etc/pam.d/` directory
  - Stores PAM config files
  - Include directives that PAM looks to for authentication

- Modules
  - Modules will generate success or failure when called
  - Account module - checks user accessibility
  - Auth - Verify passwords and set credentials (Kerberos tickets)
  - Password - Change and verify passwords
  - Session - Configure and manages user sessions

- Control flags
  - Tell PAM what to do with the result
  - Optional, required, requisite, sufficient

- Examples of PAM directives
  - Require the user to enter a strong password
    - `password requisite pam_pwquality.so local_users_only`
  - Enforce a password history of 90 days
    - `password requisite pam_pwhistory.so remember=90`
  - Allow the module not to do any password checks
    - `password sufficient pam_unix.so sha512 use_authtok`

- User lockout
  - Module `pam_failock` (newer `pam_tally2`)
    - Trigger temporary user lockout at failed user auth
  - Place user lockout directives in `/etc/pam.d/password-auth` and `/etc/pam.d/system-auth`
  - `pam_tally2 -r -u user` - Unlock user and reset failure count

- `/etc/securetty` - Determines the controlling terminals the root user has access to

### Public Key Infrastructure (PKI)

- PKI is a framework used to create, manage, distribute, use, store, and
  revoke digital certificates and manage public-key encryption.

- Publicly available or maintained privately by an organization

- PKI Components
  - Digital Signature
    - Encrypted message digest with a user's private key
  - Digital Certificate
    - Electronic document that associates credentials with a public key
  - Certificate Authority (CA)
    - Issues digital certificates for entities and maintains the
          associated private/public key pair
  - Certificate Signing Request (CSR)
    - Message sent to the certificate authority in which an entity applies
          for a certificate

- OpenSSL
  - Open-source implementation of the SSL/TLS protocol for securing data
      in transit using cryptography
  - Most common tools for generating and managing components of a PKI
  - `openssl [subcommand] [options]`

- OpenVPN
  - Supports password-based certificate-based, and smart card-based authentication
      for clients
  - Configure in `/etc/openvpn/` directory

## SELinux and AppArmor

## Firewalls

- Program interface between private network and the internet
- Firewall can accept, reject, or drop (no notification back) connections/requests
- Types
  - Packet Filter Firewall (1st Gen)
    - Decisions based on rules that correspond to network packet attributes
    - "Sateless firewalls" - Only instpect packet in isolation

  - Stateful Firewalls (2nd Gen)
    - Identifies past traffic related to a packet

  - Application Layer Firewall (3rd Gen)
    - Inspect the contents of application layer traffic
    - Insect HTTP or FTP

  - Stateless Firewall's ACL
    - Allows or denies packets based on various factors

### `iptables`

- Applies to a certain context and consists of rule sets (chains)
- `iptables [options] [-t table] [commands] {chain/rule specification}`
- Has 5 default tables that can be activated in Linux kernel
    1.*Filter table* - Default table. Typical packet filtering functionality.
    2.*Nat table* - Implement Network Address Translation (NAT) rules. Public Network <-> Private Network
    3.*Mangle table* - Alter the packets' TCP/IP header.
    4.*Raw table* - Configure exceptions involved in connection tracking
    5.*Security table* - Mark packets with SELinux security contexts
- By default, rules are lost on reboot, however can save explicitly with these:
  - CentOS/RHEL - `iptables-services` package
  - Debian-based (ie. Ubuntu) - `iptables-persistent` package
- Logging
  - `iptables -N LOGCHN` - Creates a new log chain
  - `iptables -I LOGCHN -j LOG` - Log all packets that reach this chain
  - Events written to `/var/log/messages` or `/var/log/kern.log`

### `ufw`

Uncomplicated Firewall (UFW) tool

- Makes iptables service easier to configure
- Examples:
  - `ufw enable` - Enable the firewall
  - `ufw allow http/tcp` - Allow rule for HTTP
  - `ufw logging`
    - Turn on logging
    - Adjust logging level: `ufw logging [level]` (ie. `low`, `medium`, `high`, `full`)
    - Logs can typicall be found in `/var/log/syslog` and `/var/log/ufw.log`
    - View with `sudo grep UFW /var/log/syslog`
- `/etc/default/ufw` file
  - Use to setup for more complicated firewalls
  - Policy defaults and kernel module usage
- `/etc/ufw/` directory
  - Granular UFW configuration files

### firewalld

Tool to dynamically manage a firewall without requiring a restart

- Uses zones and services
- Firewall zones
  - Rule sets that apply to network interfaces (ie. network interface card)
  - `drop` - Zone with lowest level of trust
- Ubuntu installation
  - `sudo apt install firewalld`
- `firewall-cmd` CLI tool
  - Configure firewalld by querying, adding, modifying, and deleting
      zones and services as desired
- By default, there is always a `public` zone
- `dmz` zone typically used for internet-facing services
- Examples:
  - `firewall-cmd --get-zones` - List available firewalld zones
  - `firewall-cmd  --permanent --zone=public --add-service=ssh` - Add SSH protocol permanently
  - `firewall-cmd --permanent --add-port=2222/tcp - Allow a specific port/protocol
  - `firewall-cmd --set-default-zone=drop` - Set a default zone. Drop will drop all incoming traffic
  - `firewall-cmd --zone=dmz -remove-port=21/tcp` - Remove FTP from the DMZ zone
  - `firewall-cmd --reload` - Reload all firewalld rules

### Netfilter

- Handles packets that traverse a network interface
- `nftables` designed as replacement for `iptables` and installed on Debian systems

- IP Forwarding - Enables incoming traffic on one network interface to another
- IP Sets
  - Collection of IP and MAC addresses, network ranges, port numbers, and network interface names
  - `ipset` - Create and modify IP sets

- Trusted ports
  - Port 0->1023
  - Must have superuser privellages

### Intrusion Prevention System (IPS)

Monitors and evaluates a system for attack signs and blocks traffic that it determines malicious

- Second layer of defence after firewall
- `DenyHosts`
  - Examine auth log files for issues
  - Protects SSH servers from brute force password cracking attacks
  - `/etc/denyhosts.conf` - primary config file
- `fail2ban`
  - Install: `sudo apt install fail2ban`
  - Examine auth log files for issues
  - Looks at any system service not just SSH
  - `/etc/fail2ban/jail.conf`
    - Primary configuration file
    - Copy primary config file to `/etc/fail2ban/jail.local`
      - `sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`
    - Or make custom `.conf` file within `/etc/fail2ban/jail.d/` directory
    - Configuration options:
      - `bantime` - How long a host is blocked from accessing a resource
      - `maxretry` - Number of times a host can fail before being blocked
      - `ignoreip` - Whitelist of accepted hosts
      - `banaction` - What to do when banned
        - Can work with `firewalld`: `banaction = firewallcmd-ipset`
    - Configuration file example:

      - ```makefile
            [sshd]
            enabled = true
            port = 22
            filter = sshd
            logpath = /var/log/auth.log  # This path may differ based on your Linux distribution.
            maxretry = 5                 # How long a host is blocked from accessing a resource
            bantime = 600                # How long a host is blocked from accessing a resource
        ```

  - `fail2ban-client status`
    - Check status of all fail2ban jails
    - `fail2ban-client status [service]` - Check status of specific jail (ie. `sshd`)

## Logging Services

Any action from OS events to user actions is logged on a Linux system

- System logs
  - System activity

- Remote logging
  - Centralized logging server that receives and processes syslog data

- syslog-ng is next generation of syslogd

- `journalctl`
  - Enables viewing and querying of log files
  - Examples:
    - `journalctl -b -1` - Show all messages from last boot
    - `journalctl -f` - Actively follow messages
    - `journalctl -u <UNIT>` - Show messages from specific service unit (ie. sshd)
    - `journalctl -n 10` - Only show 10 log lines
  - `/etc/systemd/journald.conf` - Configuration file

### `/var/log/` directory

Holds all logging files

- `/var/log/syslog` - All system events (Debian-based Linux)
- `/var/log/auth.log` - Authentication messages (Debian-based Linux)
- `/var/log/messages` - Red Hat/CentOS non-critical system event logs (RedHat/CentOS)
- `/var/log/secure` - Authentication messages (RedHat/CentOS)
- `/var/log/kern.log` - Linux kernel messages
- `/var/log/[APPLICATION]` - Misc. Application (cron, firewalld, mailog, etc)

### Log Rotation

Creating new versions of a log file. Typically compressing older logs.

- `logrotate`
  - Perform automatic rotation of logs
  - `/etc/logrotate.d/` directory - Log rotation behavior
  - Example of log rotation config file for `/etc/logrotate.d/firewalld`

    - ```txt

        /var/log/firewalld {
            weekly            <---- Time period
            missingok
            rotate 4          <---- Maximum number of files to keep
            copytruncate
            minsize 1M        <---- Minimum log file size
        }
        ```

### `rsyslogd` Service

- `/etc/rsyslog.conf`
  - Configuration for rsyslogd
  - May also be found in `/etc/rsyslog.d/50-default.conf`
  - Two-columns
    - Column 1 - Message sevirities for services (ie. info, warn, error, etc)
    - Column 2 - What actions should be taken (ie. warn user, store in log file)

## Backup, Restore, and Verify Data

- `tar`
  - "Tape archiver"
  - Creation of archives
  - `tar -cvf <FILE> --diredctory=<PATH>` - Create gzipped archive from directory
  - `tar -xvf <FILE>` - Extract compressed archive file

- `dar`
  - "Disk archiver:
  - OFfers more backup and archiving functions
  - `dar -R mydata -c full.bak` - Full backup
  - `dar -R mydata -c diff1.back -A full.back` - Differential backup (compare to last full backup)

- `cpio`
  - Copies files in and out of archives
  - Doesn't compress items, but can be used with `gzip`
  - Typically `tar` and `gzip` are more popular for archiving
  - `ls | cpio -o > dir_archive` - Copy all files in current directory to archive


- `dd`
  - "Disk duplicate" or "Disk destroyer"
  - Copies and converts fiels to be transferred from one type of media to another
  - Very powerful command
  - Options:
    - `if={filename}` - Data input to be read (can be device)
    - `of={filename}` - Data output target to be written to (can be device)
    - `bs={bytes}` - Total block size to read and write in bytes
    - `count={count}` - Number of blocks to be written
    - `status={level}` - Info to print to standard error
  - Examples:
    - `dd if={{path/to/file.iso}} of=/dev/{{usb_drive}}` - Make bootable USB from ISO
    - `dd if=/dev/sda of=/home/ismet/backup/sda_backup.img` - Make drive backup to image file
    - `dd if=/home/ismet/backup/sda_backup.img of=/dev/sda` - Restore a driave from image file

- `mirrorvg`
  - Copies all logical volumes in a specified logcial volume group for LVM
  - Can also use `mklvcopy` or `lvcreate -m1`

- Ensure good off-site backup in another location

- `scp` - Copy data to or from a remote host over SSH

- `rsync`
  - Copy files locally and to remote systems
  - Copies differences between files (differential backup)

- `xz` make smaller archives than `gzip`, but `gzip` is faster

## Hashing for Integrity Check

- Hash all files in a directory
  - `sha256sum my_dir/* > hashes.txt`
  - Example content:

    - ```txt
        250c061c02be20d0a84d91e581ea537d2f24f79c58f1abfddc1bfc78bd4d7514  temp_site/astro.config.mjs
        e94517a99de77a9ed069806a9a63511cb2b7ba945b751d3587134bb6a007e9ae  temp_site/LICENSE
        064ef947df5eaf39e7d58148293aafc40c3090d4aa19bbe67a766eb1dcb0764a  temp_site/package.json
        08d9f10cea00761f37fdd03a43ff1683f2a86c29d63f208992eed2c5818e16ed  temp_site/package-lock.json
        4d0aa23639dfadfaea4228245915c8a9b399586d028d138c09a957adced4a9a7  temp_site/README.md
        634d86e5196fa02e44122239efc8040b417881732d63c3f114c5f87f18c19a30  temp_site/sandbox.config.json
        70e9b27728abe6fba4cd7a5eaa1a8ac07cc6d2986fcbda37377636e1218d35bf  temp_site/tsconfig.json
        ```

- Check hashes in the hashes are valid, and files did not change
  - `sha256sum --check hashes.txt`
  - Example output (one file changed):

    - ```txt
        temp_site/astro.config.mjs: OK
        temp_site/LICENSE: FAILED
        temp_site/package.json: OK
        temp_site/package-lock.json: OK
        temp_site/README.md: OK
        temp_site/sandbox.config.json: OK
        temp_site/tsconfig.json: OK
        sha256sum: WARNING: 1 computed checksum did NOT match
        ```

## Backup, Restore, Synchronize

## Compressing Files

## Itengrity Checking


# MISC

## Cron

```txt
* * * * *  command to execute
┬ ┬ ┬ ┬ ┬
│ │ │ │ │
│ │ │ │ └───── Day of the week (0 - 7, where 0 and 7 represent Sunday)
│ │ │ └────────── Month (1 - 12)
│ │ └─────────────── Day of the month (1 - 31)
│ └──────────────────── Hour (0 - 23)
└───────────────────────── Minute (0 - 59)
```

- `0 * * * * /path/to/script.sh` - Beginning of every hour
- `45 4 1,15 * 5 command` - 4.45am, 1st and 15th of month, every month, only on Fridays
- `*/10 **** command` - Every 10 minutes
