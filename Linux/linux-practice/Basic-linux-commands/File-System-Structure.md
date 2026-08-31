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

### Touch Command
- **Command**: `touch demofile.txt`
- **Explanation**: Creates an empty file
- **Output**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ ls
  demofile.txt  newfile.txt  shell-scripts  testfolder1
  ```

### Echo Command
- **Command**: `echo "Hi Bandhu"`
- **Explanation**: Prints text to the terminal
- **Output**:
  ```bash
  Hi Bandhu
  ```

- **Command**: `echo "Hi Bandhu" > demofile.txt`
- **Explanation**: Creates a file and writes text to it
- **Output**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cat demofile.txt 
  Hi Bandhu
  ```

- **Command**: `echo "writing inside my test file" > myfile.txt`
- **Explanation**: Creates a file and writes text to it
- **Output**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ ls
  demofile.txt  myfile.txt  newfile.txt  shell-scripts  testfolder1
  ```

### Cat Command
- **Command**: `cat myfile.txt`
- **Explanation**: Displays file contents
- **Output**:
  ```bash
  writing inside my test file
  ```

- **Command**: `echo "additional text" >> myfile.txt`
- **Explanation**: Creates a file and writes text to it
- **Output**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ ls
  demofile.txt  myfile.txt  newfile.txt  shell-scripts  testfolder1
- **Command**: `cat myfile.txt`
- **Explanation**: Displays file contents
- **Output**:
  ```bash
  writing inside my test file
  additional text
  ```

### Vim Command
- **Command**: `vim myfile.txt`
- **Explanation**: Opens file for editing
- **Output**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cat myfile.txt 
  line 1 for head - line 10 for tail
  line 2 for head - line 9 for tail
  line 3 for head - line 8 for tail
  line 4 for head - line 7 for tail
  line 5 for head - line 6 for tail
  line 6 for head - line 5 for tail
  line 7 for head - line 4 for tail
  line 8 for head - line 3 for tail
  line 9 for head - line 2 for tail
  line 10 for head - line 1 for tail
  ```

### Head Command
- **Command**: `head myfile.txt`
- **Explanation**: Shows first 10 lines of a file
- **Output**:
  ```bash
  line 1 for head - line 10 for tail
  line 2 for head - line 9 for tail
  line 3 for head - line 8 for tail
  line 4 for head - line 7 for tail
  line 5 for head - line 6 for tail
  line 6 for head - line 5 for tail
  line 7 for head - line 4 for tail
  line 8 for head - line 3 for tail
  line 9 for head - line 2 for tail
  line 10 for head - line 1 for tail
  ```

### Tail Command
- **Command**: `tail myfile.txt`
- **Explanation**: Shows last 10 lines of a file
- **Output**:
  ```bash
  line 1 for head - line 10 for tail
  line 2 for head - line 9 for tail
  line 3 for head - line 8 for tail
  line 4 for head - line 7 for tail
  line 5 for head - line 6 for tail
  line 6 for head - line 5 for tail
  line 7 for head - line 4 for tail
  line 8 for head - line 3 for tail
  line 9 for head - line 2 for tail
  line 10 for head - line 1 for tail
  ```

- **Command**: `tail -5 myfile.txt`
- **Explanation**: Shows last 5 lines of a file
- **Output**:
  ```bash
  line 6 for head - line 5 for tail
  line 7 for head - line 4 for tail
  line 8 for head - line 3 for tail
  line 9 for head - line 2 for tail
  line 10 for head - line 1 for tail
  ```

### Real-time Monitoring with Tail
- **Command**: `tail -f myfile.txt`
- **Explanation**: Watches and displays live updates to a file
- **Output**:
  ```bash
  line 1 for head - line 10 for tail
  line 2 for head - line 9 for tail
  line 3 for head - line 8 for tail
  line 4 for head - line 7 for tail
  line 5 for head - line 6 for tail
  line 6 for head - line 5 for tail
  line 7 for head - line 4 for tail
  line 8 for head - line 3 for tail
  line 9 for head - line 2 for tail
  line 10 for head - line 1 for tail
  ```
Such commands are useful for real-time monitoring of files, allowing you to see changes as they occur. The `-f` option in `tail` stands for "follow," which means it will keep watching the file and updating the output as new lines are added. This is particularly useful for monitoring log files, system processes, or any other file that changes over time.

