# Goal is to mention all the Linux practice mistakes to avoid and how to fix them.

## Linux Practice Mistakes 

---

- **Mistake**: Using the wrong command.
  - **Description**: For example, typing `ppwd` instead of `pwd`.
  - **Fix**: Ensure you are using the correct command. You can check available commands with `man` or `--help`.

---

- **Mistake**: Not using proper directory paths.
  - **Description**: For example, using relative paths incorrectly.
  - **Fix**: Use absolute paths when necessary, or double-check your current directory with `pwd`.

---

- **Mistake**: Incorrect use of wildcards.
  - **Description**: For example, using `*` in the wrong place.
  - **Fix**: Understand the behavior of wildcards and ensure they are used correctly.

---

- **Mistake**: Forgetting to use sudo.
  - **Description**: For example, trying to modify a system file without `sudo`.
  - **Fix**: Use `sudo` to run commands that require elevated permissions.

---

- **Mistake**: Not checking error messages.
  - **Description**: For example, ignoring error messages that could indicate a mistake.
  - **Fix**: Always read and understand error messages, as they provide valuable information on what went wrong.

---

- **Mistake**: Using incorrect flags or options.
  - **Description**: For example, using `-r` instead of `-R` for recursive operations.
  - **Fix**: Refer to the manual pages (`man`) for the correct flags and options.

---

- **Mistake**: Not saving work.
  - **Description**: For example, making changes and forgetting to save.
  - **Fix**: Use `Ctrl + S` to save your work, or use a version control system like Git.

---

- **Mistake**: Using `htop` which is not installed.
  - **Description**: For example, typing `htop` instead of using `top`.
  - **Fix**: Install `htop` using `sudo apt install htop`.

---

- **Mistake**: Typing `cd /` instead of `cd ~` to return to the home directory.
  - **Description**: Forgetting to use `~` as a shorthand for the home directory.
  - **Fix**: Always use `~` or `cd` without any arguments to return to the home directory.

---

- **Mistake**: Forgetting to use `chmod` to change file permissions.
  - **Description**: Trying to run a script without ensuring it has the correct permissions.
  - **Fix**: Use `chmod +x script.sh` to make a script executable before running it.

---

- **Mistake**: Using `rm -rf` without confirmation.
  - **Description**: Accidentally removing a directory and its contents without being prompted.
  - **Fix**: Always use `rm -rf` with the `-i` option for interactive confirmation, e.g., `rm -rfi directory/`.

---

- **Mistake**: Not using `grep` to search for text within files.
  - **Description**: Trying to find text in files without using `grep`.
  - **Fix**: Use `grep "search_term" file.txt` to search for text within a file.

---

- **Mistake**: Using `sudo` for commands that don't require it.
  - **Description**: Overusing `sudo` for simple tasks that don't need elevated permissions.
  - **Fix**: Only use `sudo` when necessary to ensure that only authorized users can perform certain actions.

---

- **Mistake**: Not using `alias` to create shortcuts for commonly used commands.
  - **Description**: Repeatedly typing long or complex commands.
  - **Fix**: Create aliases in your shell configuration file (e.g., `.bashrc` or `.zshrc`) to create shortcuts for frequently used commands.

---

- **Mistake**: Using `cat` to view large files.
  - **Description**: Trying to view large files with `cat`, which can cause the terminal to freeze.
  - **Fix**: Use `less` or `more` to view large files interactively, e.g., `less file.txt`.

---

- **Mistake**: Not using `ln` to create symbolic links.
  - **Description**: Having to navigate to the original file for common operations.
  - **Fix**: Create symbolic links using `ln -s /path/to/original /path/to/link` to create shortcuts to files and directories.

---

- **Mistake**: Using the `rm` Command to Remove a Non-Empty Directory
    - **Description**: For example, typing `rm directory/` instead of `rm -r directory/`.
    - **Fix**: Use `rm -r` to remove a directory and its contents, or use `rm -rf` with interactive confirmation if you want to be prompted before each deletion.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ rm -r directory/
    user@Machine:~/Downloads/devops-notes/test$ rm -rfi directory/
    ```

---

- **Mistake**: Using absolute paths when creating symbolic links.
    - **Description**: Creating soft links with hardcoded absolute paths (e.g., /home/user/...) that immediately break when the project directory is moved, shared, or deployed to a cloud server with a different user structure.
    - **Fix**: Use relative paths when creating symbolic links within the same project tree, or ensure absolute paths match the target environment structure.
    ```bash
    ln -s ../target/file.txt link-name
    ```

---

- **Mistake**: Overwriting configuration or log files with output redirection (>).
    - **Description**: Using single redirection (>) instead of double redirection (>>), which completely overwrites and truncates existing file contents instead of appending to them.
    - **Fix**: Always use >> when appending data or logs, and double-check file redirection commands.
    ```bash
    echo "new log entry" >> application.log
    ```

---

- **Mistake**: Failing to verify the current working directory before running recursive deletions.
    - **Description**: Executing commands like rm -rf without running pwd first, resulting in the accidental deletion of critical infrastructure directories or project files.
    - **Fix**: Always run pwd or use an interactive flag (-i) before executing batch deletions.
    ```bash
    pwd
    rm -ri unwanted_folder/
    ```

---
   
- **Mistake**: Neglecting file ownership (chown) alongside permissions (chmod) for system services.
    - **Description**: Fixing permission errors with chmod 777 without adjusting user/group ownership, which creates severe security vulnerabilities in cloud environments.
    - **Fix**: Set appropriate least-privilege permissions and correct ownership using chown.
    ```bash
    sudo chown www-data:www-data /var/www/html/index.php
    sudo chmod 644 /var/www/html/index.php
    ```

---

- **Mistake**: Confusing filesystem disk space (df) with directory size (du).
    - **Description**: Trying to troubleshoot disk space alerts by only checking df -h, missing specific bloated directories or hidden log files filling up storage.
    - **Fix**: Use du -sh to inspect directory-level disk consumption.
    ```bash
    du -sh /var/log/*
    ```

---

- **Mistake**: Thinking Linux is a single operating system: Failing to recognize that Linux is actually a kernel and that there are multiple Distributions (Distros) like Ubuntu, Red Hat, and Debian that package it with different tools.

---

- **Mistake**: Allocating 100% of RAM to a Virtual Machine: Assigning all physical system memory to the guest OS without keeping sufficient RAM for the host computer and hypervisor.

---

- **Mistake**: Using Windows-style backslashes: Typing backslashes (\) instead of forward slashes (/) when specifying Linux file paths.

---

- **Mistake**: Confusing root with /: Mistaking the root user's home directory (root) for the absolute top-level base of the file system (/)

---


- **Mistake**: Forgetting to update package lists: Attempting to install software packages without first executing sudo apt update, which frequently leads to "File Not Found" errors for outdated package records

---
- **Mistake**: Running everything as the Root user: Operating as the superuser for routine tasks instead of using a standard user account and invoking sudo only when elevated privileges are required.

---
- **Mistake**: Losing custom environment variables: Expecting variables set via export to persist after closing the terminal window rather than adding them permanently to configuration files like .bashrc.

---
- **Mistake**: Confusing private and public IP addresses: Mixing up local, private network addresses (such as 192.168...) with public internet IP addresses.

---

- **Mistake**: Sharing the SSH private key: Exposing or sharing the private cryptographic key rather than treating it as a secret identity and distributing only the public key.

---
