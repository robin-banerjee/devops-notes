# Directory and File Operations

This section documents various Linux commands and operations related to directories and files.

## Creating Directories

- **mkdir**: Create a new directory.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mkdir devops
  ```

## Listing Directory Contents

- **ls**: List the contents of a directory.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ ls
  ```

## Changing Directories

- **cd**: Change the current directory.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cd devops
  ```

## Copying Files and Directories

- **cp**: Copy files and directories.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cp newfile.txt devops/
  ```

## Moving Files and Directories

- **mv**: Move or rename files and directories.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mv newfile.txt ../cloud/
  ```

## Removing Files and Directories

- **rm**: Remove files.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ rm newfile.txt
  ```

- **rmdir**: Remove empty directories.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ rmdir devops
  ```

- **rm -r**: Remove directories and their contents.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ rm -r devops
  ```

## Creating and Editing Files

- **touch**: Create an empty file.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ touch devops-file.txt
  ```

- **cat**: Display the contents of a file.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cat myfile.txt
  ```

- **less**: Display the contents of a file in a pager.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ less myfile.txt
  ```

- **tail -f**: Continuously display the contents of a file as it is updated.
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ tail -f myfile.txt
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
  ^C
  ```

## Terminal Outputs

Here are some example terminal outputs for the commands described above:

- **mkdir devops**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mkdir devops
  ```

- **ls**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ ls
  demofile.txt  devops  myfile.txt  newfile.txt  shell-scripts  testfolder1
  ```

- **cd devops**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cd devops
  ```

- **cp newfile.txt devops/**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cp newfile.txt devops/
  ```

- **mv newfile.txt ../cloud/**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mv newfile.txt ../cloud/
  ```

- **mv devops/ linux-for-devops**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mv devops/ linux-for-devops
  ```

- **cat myfile.txt**:
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

- **less myfile.txt**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ less myfile.txt
  ```

- **tail -f myfile.txt**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ tail -f myfile.txt
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
  ^C
  ```

- **cp -r cloud/ devops/**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ cp -r cloud/ devops/
  ```

- **mv newfile.txt ../cloud/**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mv newfile.txt ../cloud/
  ```

- **mv devops/ linux-for-devops**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ mv devops/ linux-for-devops
  ```

- **rm newfile.txt**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ rm newfile.txt
  ```

- **rmdir devops**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ rmdir devops
  ```

- **rm -r devops**:
  ```bash
  user@Machine:~/Downloads/devops-notes/test$ rm -r devops
  ```

# wc

The `wc` command is used to count the number of lines, words, and bytes in a file.

## Example

```sh
$ wc myfile.txt
```

### Output

```
10  90 342 myfile.txt
```

- **Lines**: 10 # number of lines in the file
- **Words**: 90 # number of words in the file
- **Bytes**: 342 # number of bytes in the file

