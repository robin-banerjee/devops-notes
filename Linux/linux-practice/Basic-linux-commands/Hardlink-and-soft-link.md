# Goal is to understand difference between hard link and soft link in linux

# Hardlink and Soft Link

In Linux, a **hard link** is a link to a file that refers to the same inode. It allows multiple names for the same file. A **soft link** (or symbolic link) is a link to another file or directory. It can point to a file or directory that does not yet exist.

## Hardlink

A hard link is created using the `ln` command.

### Example

```sh
$ ln linux-for-devops/cloud/devops-file.txt hardlink-file
```

### Output

```sh
$ cat hardlink-file
hi bandhu... this is hardlink
```

### Behavior

- Deleting the original file does not delete the hard link. The file content remains until all links are removed.
- Deleting a hard link does not delete the file content until the last link is removed.

## Soft Link (Symbolic Link)

A soft link is created using the `ln -s` command.

### Example

user@Machine:~/Downloads/devops-notes$ cd test/
user@Machine:~/Downloads/devops-notes/test$ ls
cloud  demofile.txt  linux-for-devops  myfile.txt  newfile.txt  shell-scripts  testfolder1
user@Machine:~/Downloads/devops-notes/test$ cd linux-for-devops/
user@Machine:~/Downloads/devops-notes/test/linux-for-devops$ ls
cloud  devops-file.txt
user@Machine:~/Downloads/devops-notes/test/linux-for-devops$ cd cloud/
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ ls
devops-file.txt
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ echo "hello bandhu... this is soft link" > devops-file.txt 
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ cat devops-file.txt 
hello bandhu... this is soft link
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ pwd
/home/user/Downloads/devops-notes/test/linux-for-devops/cloud
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ cd 
user@Machine:~$ pwd
/home/user
user@Machine:~$ cd Downloads/devops-notes/test/
user@Machine:~/Downloads/devops-notes/test$ ls 
cloud  demofile.txt  linux-for-devops  myfile.txt  newfile.txt  shell-scripts  testfolder1
user@Machine:~/Downloads/devops-notes/test$ ls -l
total 24
drwxrwxr-x 2 user user 4096 Aug 31 19:30 cloud
-rw-rw-r-- 1 user user   10 Aug 31 17:19 demofile.txt
drwxrwxr-x 3 user user 4096 Aug 31 19:30 linux-for-devops
-rw-rw-r-- 1 user user  342 Aug 31 17:28 myfile.txt
-rw-rw-r-- 1 user user    0 Aug 29 19:32 newfile.txt
drwxrwxr-x 2 user user 4096 May 24 12:38 shell-scripts
drwxrwxr-x 3 user user 4096 May 27 17:46 testfolder1
user@Machine:~/Downloads/devops-notes/test$ ln -s /home/user/Downloads/devops-notes/test/linux-for-devops/cloud/devops-file.txt softlink-file
user@Machine:~/Downloads/devops-notes/test$ cd ..
user@Machine:~/Downloads/devops-notes$ cd test/
user@Machine:~/Downloads/devops-notes/test$ ls -l
total 28
drwxrwxr-x 2 user user 4096 Aug 31 19:30 cloud
-rw-rw-r-- 1 user user   10 Aug 31 17:19 demofile.txt
drwxrwxr-x 3 user user 4096 Aug 31 19:30 linux-for-devops
-rw-rw-r-- 1 user user  342 Aug 31 17:28 myfile.txt
-rw-rw-r-- 1 user user    0 Aug 29 19:32 newfile.txt
drwxrwxr-x 2 user user 4096 May 24 12:38 shell-scripts
lrwxrwxrwx 1 user user   77 Aug 31 20:30 softlink-file -> /home/user/Downloads/devops-notes/test/linux-for-devops/cloud/devops-file.txt
drwxrwxr-x 3 user user 4096 May 27 17:46 testfolder1
user@Machine:~/Downloads/devops-notes/test$ cat softlink-file 
hello bandhu... this is soft link
user@Machine:~/Downloads/devops-notes/test$ echo "testing if softlink file updates" 
testing if softlink file updates
user@Machine:~/Downloads/devops-notes/test$ cd linux-for-devops/cloud/
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ echo "testing if softlink file updates" >> devops-file.txt 
user@Machine:~/Downloads/devops-notes/test/linux-for-devops/cloud$ cd ../..
user@Machine:~/Downloads/devops-notes/test$ pwd
/home/user/Downloads/devops-notes/test
user@Machine:~/Downloads/devops-notes/test$ l
cloud/  demofile.txt  linux-for-devops/  myfile.txt  newfile.txt  shell-scripts/  softlink-file@  testfolder1/
user@Machine:~/Downloads/devops-notes/test$ ls
cloud  demofile.txt  linux-for-devops  myfile.txt  newfile.txt  shell-scripts  softlink-file  testfolder1
user@Machine:~/Downloads/devops-notes/test$ cat softlink-file 
hello bandhu... this is soft link
testing if softlink file updates
user@Machine:~/Downloads/devops-notes/test$ rm linux-for-devops/cloud/devops-file.txt 
user@Machine:~/Downloads/devops-notes/test$ ls -l
total 28
drwxrwxr-x 2 user user 4096 Aug 31 19:30 cloud
-rw-rw-r-- 1 user user   10 Aug 31 17:19 demofile.txt
drwxrwxr-x 3 user user 4096 Aug 31 19:30 linux-for-devops
-rw-rw-r-- 1 user user  342 Aug 31 17:28 myfile.txt
-rw-rw-r-- 1 user user    0 Aug 29 19:32 newfile.txt
drwxrwxr-x 2 user user 4096 May 24 12:38 shell-scripts
lrwxrwxrwx 1 user user   77 Aug 31 20:30 softlink-file -> /home/user/Downloads/devops-notes/test/linux-for-devops/cloud/devops-file.txt
drwxrwxr-x 3 user user 4096 May 27 17:46 testfolder1
user@Machine:~/Downloads/devops-notes/test$ ls
cloud  demofile.txt  linux-for-devops  myfile.txt  newfile.txt  shell-scripts  softlink-file  testfolder1
user@Machine:~/Downloads/devops-notes/test$ l
cloud/  demofile.txt  linux-for-devops/  myfile.txt  newfile.txt  shell-scripts/  softlink-file@  testfolder1/
user@Machine:~/Downloads/devops-notes/test$ cat softlink-file 
cat: softlink-file: No such file or directory
user@Machine:~/Downloads/devops-notes/test$ touch linux-for-devops/cloud/devops-file.txt
user@Machine:~/Downloads/devops-notes/test$ echo "hi bandhu... this is hardlink" > linux-for-devops/cloud/devops-file.txt 
user@Machine:~/Downloads/devops-notes/test$ cat linux-for-devops/cloud/devops-file.txt 
hi bandhu... this is hardlink
user@Machine:~/Downloads/devops-notes/test$ ln linux-for-devops/cloud/devops-file.txt hardlink-file
user@Machine:~/Downloads/devops-notes/test$ cat hardlink-file 
hi bandhu... this is hardlink
user@Machine:~/Downloads/devops-notes/test$ cat softlink-file 
hi bandhu... this is hardlink
user@Machine:~/Downloads/devops-notes/test$ rm linux-for-devops/cloud/devops-file.txt 
user@Machine:~/Downloads/devops-notes/test$ ls
cloud         hardlink-file     myfile.txt   shell-scripts  testfolder1
demofile.txt  linux-for-devops  newfile.txt  softlink-file
user@Machine:~/Downloads/devops-notes/test$ l
cloud/        hardlink-file      myfile.txt   shell-scripts/  testfolder1/
demofile.txt  linux-for-devops/  newfile.txt  softlink-file@
user@Machine:~/Downloads/devops-notes/test$ ls -l
total 32
drwxrwxr-x 2 user user 4096 Aug 31 19:30 cloud
-rw-rw-r-- 1 user user   10 Aug 31 17:19 demofile.txt
-rw-rw-r-- 1 user user   30 Aug 31 20:40 hardlink-file
drwxrwxr-x 3 user user 4096 Aug 31 19:30 linux-for-devops
-rw-rw-r-- 1 user user  342 Aug 31 17:28 myfile.txt
-rw-rw-r-- 1 user user    0 Aug 29 19:32 newfile.txt
drwxrwxr-x 2 user user 4096 May 24 12:38 shell-scripts
lrwxrwxrwx 1 user user   77 Aug 31 20:30 softlink-file -> /home/user/Downloads/devops-notes/test/linux-for-devops/cloud/devops-file.txt
drwxrwxr-x 3 user user 4096 May 27 17:46 testfolder1
user@Machine:~/Downloads/devops-notes/test$ cat hardlink-file 
hi bandhu... this is hardlink
user@Machine:~/Downloads/devops-notes/test$ cat softlink-file 
cat: softlink-file: No such file or directory

### Behavior

- Deleting the original file breaks the soft link, making it a "dangling" link.
- Deleting a soft link does not affect the original file.

## Summary

- **Hardlink**: Links to the same inode, deleting the original file does not affect the hard link. However, deleting the hard link reduces the link count. If the link count reaches zero, the file is deleted.
- **Softlink**: Links to another file or directory, breaking the link if the original is deleted.