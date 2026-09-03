# User & Environment Information

- which : 
Locates the full file path of executable binaries in the user's $PATH.
```
which bash
which cp
which java
which python
which docker
```

- id : Displays the real and effective User ID (UID), Group ID (GID), and supplementary group memberships.
```
id
whoami 
who
who -a
```
Identifies the currently logged-in user and provides session tracking.

    whoami (Effective Username)Prints solely the username of the currently active user session.  Best used for quick identity checks in scripts, automated jobs, or terminal prompts.
    
    id (Detailed Identity & Groups)Reports the numeric User ID (UID), Group ID (GID), and all supplementary group memberships for the user.  Essential for debugging file permission errors, verifying sudo/admin access, and inspecting security contexts.
    
    who (Active System Sessions)Displays a comprehensive list of all users currently logged into the system, including their terminal lines, login timestamps, and remote host origins.  Useful for system administrators auditing concurrent access and multi-user activity.

# User Database Inspection
```
cat /etc/passwd
```
**Details: Displays local system user accounts, login shells, and home directories.**

# System Control & Package Management

- shutdown : Brings the system down securely.
```
shutdown
shutdown -c
```
Flags: -c means it Cancels a pending scheduled shutdown sequence.

# Package Management (apt, apt-get)

- Debian/Ubuntu's advanced package handling utility.
```
sudo apt-get update
sudo apt install docker.io
```

- Cross-Distribution Package Managers
Commands native to other distributions that are absent or require installation on Debian-based hosts:

    dnf / yum (Red Hat / CentOS / Fedora)

    pacman (Arch Linux)

    portage (Gentoo)

    rpm (Red Hat Package Manager)