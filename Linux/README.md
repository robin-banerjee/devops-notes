# Goal is to practice using linux commands

## Introduction to Linux Commands

Linux commands are essential for interacting with the operating system and managing files and directories. This section provides a brief overview of some commonly used Linux commands.

## Navigating the File System

- **pwd**: Prints the current working directory.
- **cd**: Changes the directory.
- **ls**: Lists directory contents.
- **mkdir**: Creates a new directory.
- **rm**: Removes a file or directory.

## Basic Terminal Output Examples

```bash
user@Machine:~/Downloads/devops-notes/Linux$ uname
Linux

user@Machine:~/Downloads/devops-notes/Linux$ hostname
Machine

user@Machine:~/Downloads/devops-notes/Linux$ whoami 
user

user@Machine:~/Downloads/devops-notes/Linux$ pwd
/home/user/Downloads/devops-notes/Linux

user@Machine:~/Downloads/devops-notes/Linux$ tree
.
├── common-linux-commands.gif
├── linux basic notes.pdf
├── Linux-Cheatsheet.pdf
├── linux-practice.md
└── Linux-Shortnotes.pdf
1 directory, 5 files
```

## System Monitoring

- **top**: Displays a dynamic real-time view of running processes.
  ```bash
    user@Machine:~/Downloads/devops-notes/Linux$ top
    top - 17:40:41 up  1:37,  1 user,  load average: 0.01, 0.05, 0.13
    Tasks: 366 total,   1 running, 365 sleeping,   0 stopped,   0 zombie
    %Cpu(s):  0.8 us,  0.5 sy,  0.0 ni, 98.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
    MiB Mem :  31193.9 total,   9077.1 free,   6214.6 used,  18065.9 buff/cache     
    MiB Swap:  20479.5 total,  20479.5 free,      0.0 used.  24979.3 avail Mem 
    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                     

   2382 user      17  -3 2138444 236920 197964 S   4.7   0.7   1:36.11 cosmic-comp                                 

   5813 user      20   0 1450.2g 375264 119288 S   3.7   1.2   1:04.96 code                                        

   5732 user      20   0 1450.4g 283024 194808 S   1.3   0.9   0:17.07 code  
   .
   .
   .
   .

  ```

## Note about PID 1:
Initial Process: The first process started during system boot.
System Management: Manages the entire system, including services and user sessions.
Service Management: Uses process managers like systemd to start and manage system services.
Signal Handling: Handles signals that affect the entire system.
Process Isolation: Ensures that processes do not interfere with each other.
Logging and Monitoring: Collects and manages system logs and events.
Example with systemd:
systemd is the process that manages PID 1.
It starts and manages system services.
It handles system boot and shutdown processes.
It ensures that all services are running correctly.
Summary:
PID 1 is crucial for system initialization and management, ensuring that all services and processes run smoothly.

- **free -h**: Shows memory usage in a human-readable format. Example:
  ```bash
    user@Machine:~/Downloads/devops-notes/Linux$ free -h

                   total        used        free      shared  buff/cache   available

    Mem:            30Gi       6.1Gi       8.9Gi       178Mi        17Gi        24Gi

    Swap:           19Gi          0B        19Gi
  ```
- **df -h**: Displays disk space usage in a human-readable format. Example:
  ```bash
    user@Machine:~/Downloads/devops-notes/Linux$ df -h
    Filesystem             Size  Used Avail Use% Mounted on

    tmpfs                  3.1G  2.1M  3.1G   1% /run

    efivarfs               128K   36K   88K  30% /sys/firmware/efi/efivars

    /dev/mapper/data-root  929G  170G  712G  20% /

    tmpfs                   16G   41M   16G   1% /dev/shm

    tmpfs                  5.0M     0  5.0M   0% /run/lock

    /dev/nvme0n1p1        1020M  445M  576M  44% /boot/efi

    /dev/nvme0n1p2         4.0G  3.4G  673M  84% /recovery

    tmpfs                   16G     0   16G   0% /run/qemu

    tmpfs                  3.1G  164K  3.1G   1% /run/user/1000
  ```

## File System Structure

- **/bin**: Essential binaries.
- **/boot**: Bootloader files.
- **/dev**: Device files.
- **/etc**: Configuration files.
- **/home**: User home directories.
- **/lib**: Libraries.
- **/media**: Mount points for removable media.
- **/mnt**: Mount points for temporary filesystems (Example: accessing files on a mounted pendrive via USB port).
- **/opt**: Optional software packages.
- **/proc**: Virtual filesystem for system information.
- **/root**: Root user's home directory.
- **/run**: Runtime variable data.
- **/sbin**: System binaries.
- **/srv**: Service data.
- **/sys**: Virtual filesystem for kernel parameters.
- **/tmp**: Temporary files.
- **/usr**: User binaries and libraries.
- **/var**: Variable data.

## Notes on Creating and Listing Folders

- **Creating a Folder**:
  - Use the `mkdir` command to create a new directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ mkdir devops
    ```

- **Listing Directory Contents**:
  - Use the `ls` command to list the contents of the current directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ ls
    devops  shell-scripts  testfolder1
    ```

- **Listing Detailed File Information**:
  - Use the `ls -l` command to display detailed information about the files and directories, including permissions, user, and group.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ ls -l
    total 12
    drwxrwxr-x 2 user user 4096 Aug 29 19:22 devops
    -rw-rw-r-- 1 user user    0 Aug 29 19:32 newfile.txt
    drwxrwxr-x 2 user user 4096 May 24 12:38 shell-scripts
    drwxrwxr-x 3 user user 4096 May 27 17:46 testfolder1
    ```

- **Understanding Permissions**:
  - The permissions `drwxrwxr-x` indicate:
    - `d`: Directory.
    - `rwx`: Read, write, and execute permissions for the owner.
    - `rwx`: Read, write, and execute permissions for the group.
    - `r-x`: Read and execute permissions for others.

- **Understanding User and Group**:
  - The user and group are listed as `user user`.
  - Both the owner and the group have read, write, and execute permissions (`rwx`).

## Notes on Creating Files

- **Creating a File**:
  - Use the `touch` command to create a new empty file.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ touch newfile.txt
    ```

- **Listing Detailed File Information**:
  - Use the `ls -l` command to display detailed information about the files and directories, including permissions, user, and group.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ ls -l
    total 12
    drwxrwxr-x 2 user user 4096 Aug 29 19:22 devops
    -rw-rw-r-- 1 user user    0 Aug 29 19:32 newfile.txt
    drwxrwxr-x 2 user user 4096 May 24 12:38 shell-scripts
    drwxrwxr-x 3 user user 4096 May 27 17:46 testfolder1
    ```

- **Understanding Permissions**:
  - The permissions `-rw-rw-r--` indicate:
    - `-`: Regular file.
    - `rw-`: Read and write permissions for the owner.
    - `rw-`: Read and write permissions for the group.
    - `r--`: Read-only permissions for others.

## Notes on Changing Directories

- **Changing to a Specific Directory**:
  - Use the `cd` command to change to a specific directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ cd devops/
    ```

- **Checking the Current Directory**:
  - Use the `pwd` command to check the current directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ pwd
    /home/user/Downloads/devops-notes/test/devops
    ```

- **Returning to the Parent Directory**:
  - Use the `cd ..` command to return to the parent directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ cd ..
    user@Machine:~/Downloads/devops-notes/test$ pwd
    /home/user/Downloads/devops-notes/test
    ```

- **Returning to the Home Directory**:
  - Use the `cd` command without any arguments to return to the home directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ cd
    user@Machine:~$ pwd
    /home/user
    ```

- **Changing to a Different Directory from Home**:
  - Use the `cd` command with the full path to change to a different directory.
    ```bash
    user@Machine:~$ cd Downloads/devops-notes/test/devops/
    user@Machine:~/Downloads/devops-notes/test/devops$ pwd
    /home/user/Downloads/devops-notes/test/devops
    ```

- **Returning Multiple Levels Up**:
  - Use multiple `cd ..` commands to return to a higher directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ cd ../..
    user@Machine:~/Downloads/devops-notes$ pwd
    /home/user/Downloads/devops-notes
    ```

- **Changing to a Subdirectory**:
  - Use the `cd` command with the subdirectory name to change to a subdirectory.
    ```bash
    user@Machine:~/Downloads/devops-notes$ cd test/devops/
    user@Machine:~/Downloads/devops-notes/test/devops$ pwd
    /home/user/Downloads/devops-notes/test/devops
    ```

- **Returning to the Parent Directory from Home**:
  - Use the `cd` command with `..` to return to the parent directory from home.
    ```bash
    user@Machine:~$ cd ../..
    user@Machine:~/Downloads/devops-notes$ pwd
    /home/user/Downloads/devops-notes
    ```

These notes provide a basic understanding of how to navigate the file system using the `cd`, `pwd`, and `~` commands, including changing to different directories, returning to the parent and home directories, and navigating multiple levels up and down the directory structure.

## Notes on Creating, Listing, and Removing Files and Directories

- **Creating a File**:
  - Use the `touch` command to create a new empty file.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ touch devops_file.txt
    ```

- **Listing Directory Contents**:
  - Use the `ls` command to list the contents of the current directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ ls
    devops_file.txt
    ```

- **Removing a File**:
  - Use the `rm` command to remove a file.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ rm devops_file.txt
    ```

- **Listing Directory Contents After Removing a File**:
  - Use the `ls` command to confirm that the file has been removed.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ ls
    ```

- **Changing to a Different Directory**:
  - Use the `cd` command to change to a different directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test/devops$ cd ..
    user@Machine:~/Downloads/devops-notes/test$ pwd
    /home/user/Downloads/devops-notes/test
    ```

- **Creating a New Directory**:
  - Use the `mkdir` command to create a new directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ mkdir cloud
    ```

- **Listing Directory Contents After Creating a New Directory**:
  - Use the `ls` command to confirm that the directory has been created.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ ls
    cloud  devops  newfile.txt  shell-scripts  testfolder1
    ```

- **Removing a Directory**:
  - Use the `rm -r` command to remove a directory and its contents.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ rm -r cloud/
    ```

- **Listing Directory Contents After Removing a Directory**:
  - Use the `ls` command to confirm that the directory has been removed.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ ls
    devops  newfile.txt  shell-scripts  testfolder1
    ```

- **Removing an Empty Directory**:
  - Use the `rmdir` command to remove an empty directory.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ rmdir devops/
    ```

- **Listing Directory Contents After Removing an Empty Directory**:
  - Use the `ls` command to confirm that the directory has been removed.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ ls
    newfile.txt  shell-scripts  testfolder1
    ```

These notes provide a basic understanding of how to create, list, and remove files and directories using the `touch`, `ls`, `rm`, and `rmdir` commands in the Linux terminal.

