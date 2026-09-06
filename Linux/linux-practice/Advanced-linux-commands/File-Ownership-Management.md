# File Permissions and Ownership Management in Linux

## Viewing Permissions (`ls -l`)

Running `ls -l` displays detailed file and directory metadata in a structured layout:

```text
-rw-rw-r-- 1 guy guest 0 Sep 3 12:36 sensitive-data.txt
│└───┬───┘ │  │   │   
│    │     │  │   └── Group Owner (`guest`)
│    │     │  └────── User Owner (`guy`)
│    │     └───────── Hard link count
│    └─────────────── Permissions string (Owner | Group | Others)
└──────────────────── File type (`-` = regular file, `d` = directory)
```

## Permission Control (chmod & umask)
- chmod (Change Mode): Modifies read (r=4), write (w=2), and execute (x=1) access rights using octal notation.

- chmod 600 sensitive-data.txt
```
    Permissions: -rw-------

    Breakdown: Owner: Read/Write (4+2=6), Group: None (0), Others: None (0).

    Use Case: Securing private keys, tokens, or sensitive files so only the owner can access them.
```

- chmod 777 testfolder2/
```
    Permissions: drwxrwxrwx

    Breakdown: Owner: Read/Write/Execute (7), Group: Read/Write/Execute (7), Others: Read/Write/Execute (7).

    Use Case: Grants complete read, write, and directory-traversal rights to all system users.
```
- umask (User Mask): Sets default permission restrictions applied to newly created files and directories.
```
    Command: umask (Outputs: 0002)

    Default Calculation:

    Files (Base 666): 666 - 002 = 664 (-rw-rw-r--)

    Directories (Base 777): 777 - 002 = 775 (drwxrwxr-x)
```
- Ownership Management (chown & chgrp)
    chown (Change Owner)
    Changes user ownership of a file or directory. Standard users cannot reassign ownership of their files to another account; administrative escalation (sudo) is mandatory.
```
    Command: sudo chown guest testfolder2
    Effect: Changes the directory user owner from guy to guest.
    Syntax: sudo chown <new_owner> <target>
```

- chgrp (Change Group): Reassigns group ownership for files or directories.
```
    Command: sudo chgrp devops sensitive-data.txt

    Effect: Changes group ownership from guy to devops.

    Syntax: sudo chgrp <new_group> <target>
```

## Practice notes

```
guy@Host:~/Downloads/devops-notes$ cd test
guy@Host:~/Downloads/devops-notes/test$ touch testfolder1/sensitive-data.txt
guy@Host:~/Downloads/devops-notes/test$ cd testfolder1/
guy@Host:~/Downloads/devops-notes/test/testfolder1$ ls -l
total 4
-rw-rw-r-- 1 guy guy    0 Sep  3 12:36 sensitive-data.txt
drwxrwxr-x 2 guy guy 4096 May 27 17:51 testfolder2

guy@Host:~/Downloads/devops-notes/test/testfolder1$ chmod 600 sensitive-data.txt 
guy@Host:~/Downloads/devops-notes/test/testfolder1$ chmod 777 testfolder2/
guy@Host:~/Downloads/devops-notes/test/testfolder1$ ls -l
total 4
-rw------- 1 guy guy    0 Sep  3 12:36 sensitive-data.txt
drwxrwxrwx 2 guy guy 4096 May 27 17:51 testfolder2

guy@Host:~/Downloads/devops-notes/test/testfolder1$ umask
0002

guy@Host:~/Downloads/devops-notes/test/testfolder1$ chown guest testfolder2
chown: changing ownership of 'testfolder2': Operation not permitted
guy@Host:~/Downloads/devops-notes/test/testfolder1$ sudo chown guest testfolder2
[sudo] password for guy: 
guy@Host:~/Downloads/devops-notes/test/testfolder1$ ls -l
total 4
-rw------- 1 guy  guy    0 Sep  3 12:36 sensitive-data.txt
drwxrwxrwx 2 guest guy 4096 May 27 17:51 testfolder2


guy@Host:~/Downloads/devops-notes/test/testfolder1$ sudo chgrp devops sensitive-data.txt 
guy@Host:~/Downloads/devops-notes/test/testfolder1$ ls -l
total 4
-rw------- 1 guy  devops    0 Sep  3 12:36 sensitive-data.txt
drwxrwxrwx 2 guest guy   4096 May 27 17:51 testfolder2
```