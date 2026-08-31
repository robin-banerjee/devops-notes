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

Note about PID 1:
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