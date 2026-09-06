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

### Practice notes for File Permissions and Ownership

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

---

# Archive and Compression Utilities in Linux

## Summary Table

| Command | Action | Key Options | Extension |
| :--- | :--- | :--- | :--- |
| **`zip`** | Creates compressed zip archives | `-r` (recursive) | `.zip` |
| **`unzip`** | Extracts files from zip archives | Standard extraction | `.zip` |
| **`tar`** | Creates or extracts compressed tape archives | `-c` (create), `-x` (extract), `-v` (verbose), `-z` (gzip), `-f` (filename) | `.tar.gz` / `.tgz` |

---

## 1. Zip & Unzip Utilities

### Creating Zip Archives (`zip`)
Compresses files and directories into a single `.zip` file.
* **Syntax:** `zip [options] <archive_name.zip> <target_file_or_directory>`
* **Example:**
  ```bash
  zip -r lfd.zip linux-for-devops
  ```
-r (Recursive): Includes all subdirectories and nested files inside the target directory.

### Extracting Zip Archives (unzip)
Uncompresses and restores files from a .zip archive into the current working directory.
* **Syntax:** `unzip <archive_name.zip>`
* **Example:**
  ```bash
  unzip lfd.zip
  ```

## 2. Tar Utilities
tar (Tape Archive) bundles multiple files into a single archive and can compress them using algorithm tools like GunZip.

### Archiving and Compressing (`tar -cvzf`)
Creates a Gzip-compressed tarball archive.
* **Syntax:** `tar -cvzf <archive_name.tar.gz> <target_directory>`
* **Example:**
  ```bash
  tar -cvzf cloud.tar.gz cloud
  ```
Flags:
- -c (create): Initiates creation of a new archive.
- -v (verbose): Lists each file on the terminal screen as it gets processed.
- -z (gzip): Filters the archive through Gzip compression.
- -f (filename): Specifies the output filename for the archive (must be placed directly before the filename).

### Extracting Compressed Tarballs (`tar -xvzf`)
Uncompresses and unpacks a .tar.gz archive into the current directory.
* **Syntax:** `tar -xvzf <archive_name.tar.gz>`
* **Example:**
  ```bash
  tar -xvzf cloud.tar.gz
  ```
Flags:
- -x (xtract): Extracts files from an existing archive.
- -v (verbose): Displays extracted file paths in real time.
- -z (gzip): Decompresses using Gzip before unpacking.
- -f (filename): Identifies the source archive file to extract.

### Practice notes for zip - unzip - tar
```Bash
# 1. Compress a directory into a zip archive
zip -r lfd.zip linux-for-devops

# 2. Extract a zip archive inside a subfolder
cp lfd.zip cloud/unzipped_files/
cd cloud/unzipped_files/
unzip lfd.zip

# 3. Create a compressed .tar.gz archive
tar -cvzf cloud.tar.gz cloud

# 4. Extract a .tar.gz archive
tar -xvzf cloud.tar.gz
```