# Users and Groups Management in Linux

## Key Configuration Files
* `/etc/passwd`: Stores local user account definitions (username, password placeholder `x`, UID, GID, user info, home directory, default shell).
* `/etc/group`: Stores group definitions (group name, password placeholder `x`, GID, comma-separated list of secondary members).

---

## User Management Commands

* **`id`**
  * **Description:** Displays the real and effective User ID (UID), primary Group ID (GID), and secondary group memberships for the current or specified user.
  * **Syntax:** `id [username]`
  * **Example:**
    ```bash
    id
    ```

* **`useradd`**
  * **Description:** Creates a new user account. Requires administrative privileges (`sudo`).
  * **Syntax:** `sudo useradd [options] <username>`
  * **Common Options:**
    * `-m`: Creates the user's home directory under `/home/<username>`.
  * **Examples:**
    ```bash
    sudo useradd -m guest
    sudo useradd guest-wife
    ```

* **`passwd`**
  * **Description:** Changes or assigns a password for a user account.
  * **Syntax:** `sudo passwd <username>`
  * **Example:**
    ```bash
    sudo passwd guest
    ```

* **`su` & `exit`**
  * **Description:** `su` (Switch User) changes the active shell context to another user. `exit` terminates the switched session and returns to the previous user.
  * **Syntax:** `su <username>`
  * **Example:**
    ```bash
    su guest
    whoami   # Outputs: guest
    exit     # Returns to original account
    ```

* **`userdel`**
  * **Description:** Deletes a user account from `/etc/passwd`. Requires `sudo`.
  * **Syntax:** `sudo userdel <username>`
  * **Example:**
    ```bash
    sudo userdel guest
    ```

---

## Group Management Commands

* **`groupadd`**
  * **Description:** Creates a new group on the system.
  * **Syntax:** `sudo groupadd <groupname>`
  * **Examples:**
    ```bash
    sudo groupadd devops
    sudo groupadd cloud
    ```

* **`gpasswd`**
  * **Description:** Administers group memberships and administration settings in `/etc/group`.
  * **Syntax & Flags:**
    * `-a <user>`: Adds a single user to a group.
    * `-d <user>`: Removes a single user from a group.
    * `-M <user1,user2...>`: Replaces/bulk-assigns the exact list of members for a group.
  * **Examples:**
    ```bash
    # Add single users
    sudo gpasswd -a guest devops
    sudo gpasswd -a guy devops

    # Bulk assign members
    sudo gpasswd -M guest-wife,guest-mom,guest-dad cloud

    # Remove a user
    sudo gpasswd -d guest devops
    ```

* **`groupdel`**
  * **Description:** Removes an existing group from the system (does not delete user accounts assigned to it).
  * **Syntax:** `sudo groupdel <groupname>`
  * **Example:**
    ```bash
    sudo groupdel cloud
    ```

---

## System Verification & Filtering

* **Inspect Accounts & Groups:**
  ```bash
  # Search for users/groups with specific UID/GID ranges (e.g., 1000+)
  cat /etc/passwd | grep x:100
  cat /etc/group | grep x:100

- Sudoers Permission Behavior: Non-root users not explicitly listed in /etc/sudoers or members of administrative groups (such as sudo or wheel) will be denied administrative execution:
`<username> is not in the sudoers file.`

---

```
User Management:

guy@Host:~/Downloads/devops-notes/test$ id
uid=1000(guy) gid=1000(guy) groups=1000(guy),4(adm),27(sudo),108(lpadmin),125(wireshark),986(ollama),995(input)
guy@Host:~/Downloads/devops-notes/test$ useradd -m guest
useradd: Permission denied.
useradd: cannot lock /etc/passwd; try again later.
guy@Host:~/Downloads/devops-notes/test$ sudo useradd -m guest
[sudo] password for guy: 
guy@Host:~/Downloads/devops-notes/test$ cd
guy@Host:~$ pwd
/home/guy
guy@Host:~$ cd ..
guy@Host:/home$ ls
guest  guy
guy@Host:/home$ passwd guest
passwd: You may not view or modify password information for guest.
guy@Host:/home$ sudo passwd guest
New password: 
Retype new password: 
passwd: password updated successfully
guy@Host:/home$ whoami
guy
guy@Host:/home$ su guest
Password: 
$ 
$ whoami
guest
$ pwd
/home
$ ls
guest  guy
$ cd guest
$ pwd
/home/guest
$ exit
guy@Host:/home$ whoami
guy
guy@Host:/home$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
guy:x:1000:1000:User:/home/guy:/bin/bash
pipewire:x:986:104:system guy for pipewire:/nonexistent:/usr/sbin/nologin
geoclue:x:120:123::/var/lib/geoclue:/usr/sbin/nologin
ollama:x:995:986::/usr/share/ollama:/bin/false
guest:x:1001:1001::/home/guest:/bin/sh
guy@Host:/home$ id
uid=1000(guy) gid=1000(guy) groups=1000(guy),4(adm),27(sudo),108(lpadmin),125(wireshark),986(ollama),995(input)
guy@Host:/home$ su guest
Password: 
$ id
uid=1001(guest) gid=1001(guest) groups=1001(guest)
$ sudo apt-get nginix
[sudo] password for guest: 
guest is not in the sudoers file.
  
guy@Host:/home$ whoami
guy
guy@Host:/home$ userdel guest
userdel: Permission denied.
userdel: cannot lock /etc/passwd; try again later.
guy@Host:/home$ sudo userdel guest
guy@Host:/home$ su guest
su: guy guest does not exist or the guy entry does not contain all the required fields
```

---

```
Group mangement:
 
guy@Host:/home$ sudo useradd guest
guy@Host:/home$ sudo useradd guest-wife
guy@Host:/home$ sudo useradd guest-mom
guy@Host:/home$ sudo useradd guest-dad

guy@Host:/home$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
guy:x:1000:1000:User:/home/guy:/bin/bash
guest:x:1001:1001::/home/guest:/bin/sh
guest-wife:x:1002:1002::/home/guest-wife:/bin/sh
guest-mom:x:1003:1003::/home/guest-mom:/bin/sh
guest-dad:x:1004:1004::/home/guest-dad:/bin/sh

guy@Host:/home$ cat /etc/passwd | grep x:100
guy:x:1000:1000:User:/home/guy:/bin/bash
guest:x:1001:1001::/home/guest:/bin/sh
guest-wife:x:1002:1002::/home/guest-wife:/bin/sh
guest-mom:x:1003:1003::/home/guest-mom:/bin/sh
guest-dad:x:1004:1004::/home/guest-dad:/bin/sh

guy@Host:/home$ sudo groupadd devops
guy@Host:/home$ cat /etc/group
...
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:

guy@Host:/home$ sudo groupadd cloud
guy@Host:/home$ cat /etc/group
...
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:
cloud:x:1006:
guy@Host:/home$ cat /etc/group | grep x:100
users:x:100:
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:
cloud:x:1006:

guy@Host:/home$ sudo gpasswd -a guest devops
Adding guy guest to group devops
guy@Host:/home$ sudo gpasswd -a guy devops
Adding guy guy to group devops
guy@Host:/home$ cat /etc/group | grep x:100
users:x:100:
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:guest,guy
cloud:x:1006:

guy@Host:~/Downloads/devops-notes/test$ whoami
guy
guy@Host:~/Downloads/devops-notes/test$ id
uid=1000(guy) gid=1000(guy) groups=1000(guy),4(adm),27(sudo),108(lpadmin),125(wireshark),986(ollama),995(input)

guy@Host:~/Downloads/devops-notes/test$ sudo useradd -m guest
[sudo] password for guy: 
guy@Host:~/Downloads/devops-notes/test$ cd
guy@Host:~$ pwd
/home/guy
guy@Host:~$ cd ..
guy@Host:/home$ ls
guest  guy
guy@Host:/home$ whoami
guy
guy@Host:/home$ passwd guest
passwd: You may not view or modify password information for guest.
guy@Host:/home$ sudo passwd guest
New password: 
Retype new password: 
Sorry, passwords do not match.
passwd: Authentication token manipulation error
passwd: password unchanged

guy@Host:/home$ cat /etc/passwd | grep x:100
guy:x:1000:1000:User:/home/guy:/bin/bash
guest:x:1001:1001::/home/guest:/bin/sh
guest-wife:x:1002:1002::/home/guest-wife:/bin/sh
guest-mom:x:1003:1003::/home/guest-mom:/bin/sh
guest-dad:x:1004:1004::/home/guest-dad:/bin/sh

guy@Host:/home$ sudo gpasswd -M guest-wife,guest-mom,guest-dad cloud
guy@Host:/home$ cat /etc/group | grep x:100
users:x:100:
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:guest,guy
cloud:x:1006:guest-wife,guest-mom,guest-dad

guy@Host:/home$ gpasswd
Usage: gpasswd [option] GROUP
Options:
  -a, --add USER                add USER to GROUP
  -d, --delete USER             remove USER from GROUP
  -h, --help                    display this help message and exit
  -Q, --root CHROOT_DIR         directory to chroot into
  -r, --remove-password         remove the GROUP's password
  -R, --restrict                restrict access to GROUP to its members
  -M, --members USER,...        set the list of members of GROUP
      --extrausers              use the extra users database
  -A, --administrators ADMIN,...
                                set the list of administrators for GROUP
Except for the -A and -M options, the options cannot be combined.

guy@Host:/home$ sudo gpasswd -d guest  devops
Removing guy guest from group devops
guy@Host:/home$ cat /etc/group | grep x:100
users:x:100:
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:guy
cloud:x:1006:guest-wife,guest-mom,guest-dad

guy@Host:/home$ sudo groupdel cloud
guy@Host:/home$ cat /etc/group | grep x:100
users:x:100:
guy:x:1000:
guest:x:1001:
guest-wife:x:1002:
guest-mom:x:1003:
guest-dad:x:1004:
devops:x:1005:guy
(notice the group called “cloud” is deleted)

guy@Host:/home$ cat /etc/passwd | grep x:100
guy:x:1000:1000:User:/home/guy:/bin/bash
guest:x:1001:1001::/home/guest:/bin/sh
guest-wife:x:1002:1002::/home/guest-wife:/bin/sh
guest-mom:x:1003:1003::/home/guest-mom:/bin/sh
guest-dad:x:1004:1004::/home/guest-dad:/bin/sh
``` 