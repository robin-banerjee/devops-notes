# Disk Space Utilization

- df: Displays filesystem disk space usage in standard blocks.

- df -h: Shows disk space in human-readable formats across all active mount points.

# Directory Size Analysis

- du .: Recursively estimates file space usage for the current directory.

- du . | sort -n: Measures and ranks directories and subdirectories numerically by disk consumption.

# Process Inspection

- ps: Reports a snapshot of current active processes.

- ps -a: Displays process information across user sessions.

- top: Provides a dynamic, real-time view of running system tasks, CPU utilization, and memory consumption.

- fuser: Identifies which processes or users are actively accessing specific files, sockets, or mount points.

# Memory Management

- fuser: Identifies which processes or users are actively accessing specific files, sockets, or mount points.

- fuser: Identifies which processes or users are actively accessing specific files, sockets, or mount points.

- free -h: Displays total, used, and available physical and swap memory in human-readable units.

- vmstat: Reports information about virtual memory, processes, paging, block I/O, and CPU activity.

- vmstat -a: Displays detailed active and inactive memory statistics.

# Background Job Execution

- nohup: Runs a command immune to terminal hangups, allowing processes to continue running after logout while redirecting output to a persistent log file.

---

Examples:

```
user@Machine:~/Downloads/devops-notes$ df
Filesystem            1K-blocks      Used Available Use% Mounted on
...

user@Machine:~/Downloads/devops-notes$ df -h
Filesystem             Size  Used Avail Use% Mounted on
...

user@Machine:~/Downloads/devops-notes$ du .
4       ./test/cloud
4       ./test/linux-for-devops/cloud
8       ./test/linux-for-devops
8       ./test/testfolder1/testfolder2
12      ./test/testfolder1
8       ./test/shell-scripts
56      ./test
...

user@Machine:~/Downloads/devops-notes$ sort du .
sort: cannot read: du: No such file or directory
user@Machine:~/Downloads/devops-notes$ du . | sort
1016    ./.git/objects/23
1056    ./.git/objects/a0
1060    ./GitHub_Actions
1112    ./.git/objects/85
...

user@Machine:~/Downloads/devops-notes$ 
                                            
user@Machine:~/Downloads/devops-notes$ ps -a
    PID TTY          TIME CMD
   2782 tty1     00:00:00 cosmic-session
   ...

user@Machine:~/Downloads/devops-notes$ fuser
No process specification given
Usage: fuser [-fIMuvw] [-a|-s] [-4|-6] [-c|-m|-n SPACE]
             [-k [-i] [-SIGNAL]] NAME...
       fuser -l
       fuser -V
Show which processes use the named files, sockets, or filesystems.

  -a,--all              display unused files too
  -i,--interactive      ask before killing (ignored without -k)
  -I,--inode            use always inodes to compare files
  -k,--kill             kill processes accessing the named file
  -l,--list-signals     list available signal names
  -m,--mount            show all processes using the named filesystems or
                        block device
  -M,--ismountpoint     fulfill request only if NAME is a mount point
  -n,--namespace SPACE  search in this name space (file, udp, or tcp)
  -s,--silent           silent operation
  -SIGNAL               send this signal instead of SIGKILL
  -u,--user             display user IDs
  -v,--verbose          verbose output
  -w,--writeonly        kill only processes with write access
  -V,--version          display version information
  -4,--ipv4             search IPv4 sockets only
  -6,--ipv6             search IPv6 sockets only
  udp/tcp names: [local_port][,[rmt_host][,[rmt_port]]]

user@Machine:~/Downloads/devops-notes$ fuser .
/home/user/:  6444c  6447c  6472c  6486c  6493c  6534c  6561c  6601c  6619c  6621c  6675c  6772c  6788c  9864c  9885c
user@Machine:~/Downloads/devops-notes$ top 
top - 07:11:00 up  1:36,  1 user,  load average: 0.20, 0.08, 0.10
Tasks: 360 total,   1 running, 359 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.1 us,  0.4 sy,  0.3 ni, 99.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem :   total,   free,    used,   buff/cache     
MiB Swap:   total,   free,       used.   avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                               
                                     
   1930 ollama    32  12 2486704  36780  24700 S   0.0   0.1   0:00.13 ollama                                                
                                      
user@Machine:~/Downloads/devops-notes$ kill -9 1930
bash: kill: (1930) - Operation not permitted

user@Machine:~/Downloads/devops-notes$ journalctl -xe
Sep 03 07:03:55 Machine wpa_supplicant[1209]: : CTRL-EVENT-SIGNAL-CHANGE above=1 signal=-76 noise=9999 txrate=97600
Sep 03 07:03:57 Machine kernel: [UFW BLOCK] IN= OUT= MAC= SRC= DS>
Sep 03 07:04:17 Machine kernel: [UFW BLOCK] IN= OUT= MAC= SRC= DS>

user@Machine:~/Downloads/devops-notes$ nohup free -h
nohup: ignoring input and appending output to 'nohup.out'

user@Machine:~/Downloads/devops-notes$ cat nohup.out 
               total        used        free      shared  buff/cache   available
Mem:            
Swap:           
user@Machine:~/Downloads/devops-notes$ free -h
               total        used        free      shared  buff/cache   available
Mem:            
Swap:           
user@Machine:~/Downloads/devops-notes$ df -h
Filesystem ...

user@Machine:~/Downloads/devops-notes$ nohup df -h
nohup: ignoring input and appending output to 'nohup.out'
user@Machine:~/Downloads/devops-notes$ cat nohup.out 
               total        used        free      shared  buff/cache   available
Mem:            
Swap:           
Filesystem...

user@Machine:~/Downloads/devops-notes$ head -n 5 nohup.out 
               total        used        free      shared  buff/cache   available
Mem:            
Swap:           
Filesystem             Size  Used Avail Use% Mounted on
tmpfs                  
user@Machine:~/Downloads/devops-notes$ vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu

user@Machine:~/Downloads/devops-notes$ vmstat -a
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa st gu

```