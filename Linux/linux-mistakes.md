# Goal is to mention all the Linux practice mistakes that you have made and how to fix them.

## Linux Practice Mistakes 

- **Mistake**: Using the wrong command.
  - **Description**: For example, typing `ppwd` instead of `pwd`.
  - **Fix**: Ensure you are using the correct command. You can check available commands with `man` or `--help`.

- **Mistake**: Not using proper directory paths.
  - **Description**: For example, using relative paths incorrectly.
  - **Fix**: Use absolute paths when necessary, or double-check your current directory with `pwd`.

- **Mistake**: Incorrect use of wildcards.
  - **Description**: For example, using `*` in the wrong place.
  - **Fix**: Understand the behavior of wildcards and ensure they are used correctly.

- **Mistake**: Forgetting to use sudo.
  - **Description**: For example, trying to modify a system file without `sudo`.
  - **Fix**: Use `sudo` to run commands that require elevated permissions.

- **Mistake**: Not checking error messages.
  - **Description**: For example, ignoring error messages that could indicate a mistake.
  - **Fix**: Always read and understand error messages, as they provide valuable information on what went wrong.

- **Mistake**: Using incorrect flags or options.
  - **Description**: For example, using `-r` instead of `-R` for recursive operations.
  - **Fix**: Refer to the manual pages (`man`) for the correct flags and options.

- **Mistake**: Not saving work.
  - **Description**: For example, making changes and forgetting to save.
  - **Fix**: Use `Ctrl + S` to save your work, or use a version control system like Git.

- **Mistake**: Using `htop` which is not installed.
  - **Description**: For example, typing `htop` instead of using `top`.
  - **Fix**: Install `htop` using `sudo apt install htop`.

- **Mistake**: Typing `cd /` instead of `cd ~` to return to the home directory.
  - **Description**: Forgetting to use `~` as a shorthand for the home directory.
  - **Fix**: Always use `~` or `cd` without any arguments to return to the home directory.

- **Mistake**: Forgetting to use `chmod` to change file permissions.
  - **Description**: Trying to run a script without ensuring it has the correct permissions.
  - **Fix**: Use `chmod +x script.sh` to make a script executable before running it.

- **Mistake**: Using `rm -rf` without confirmation.
  - **Description**: Accidentally removing a directory and its contents without being prompted.
  - **Fix**: Always use `rm -rf` with the `-i` option for interactive confirmation, e.g., `rm -rfi directory/`.

- **Mistake**: Not using `grep` to search for text within files.
  - **Description**: Trying to find text in files without using `grep`.
  - **Fix**: Use `grep "search_term" file.txt` to search for text within a file.

- **Mistake**: Using `sudo` for commands that don't require it.
  - **Description**: Overusing `sudo` for simple tasks that don't need elevated permissions.
  - **Fix**: Only use `sudo` when necessary to ensure that only authorized users can perform certain actions.

- **Mistake**: Not using `alias` to create shortcuts for commonly used commands.
  - **Description**: Repeatedly typing long or complex commands.
  - **Fix**: Create aliases in your shell configuration file (e.g., `.bashrc` or `.zshrc`) to create shortcuts for frequently used commands.

- **Mistake**: Using `cat` to view large files.
  - **Description**: Trying to view large files with `cat`, which can cause the terminal to freeze.
  - **Fix**: Use `less` or `more` to view large files interactively, e.g., `less file.txt`.

- **Mistake**: Not using `ln` to create symbolic links.
  - **Description**: Having to navigate to the original file for common operations.
  - **Fix**: Create symbolic links using `ln -s /path/to/original /path/to/link` to create shortcuts to files and directories.

- **Mistake**: Using the `rm` Command to Remove a Non-Empty Directory
    - **Description**: For example, typing `rm directory/` instead of `rm -r directory/`.
    - **Fix**: Use `rm -r` to remove a directory and its contents, or use `rm -rf` with interactive confirmation if you want to be prompted before each deletion.
    ```bash
    user@Machine:~/Downloads/devops-notes/test$ rm -r directory/
    user@Machine:~/Downloads/devops-notes/test$ rm -rfi directory/
    ```
