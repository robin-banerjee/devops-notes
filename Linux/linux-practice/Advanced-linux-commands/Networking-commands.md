# Linux Networking Commands Cheat Sheet & Practice Notes

Below is a categorized summary and quick-reference guide covering all the networking commands and tools practiced in your session.

| Tool Category | Command | Description | Example |
| :--- | :--- | :--- | :--- |
| **Connectivity** | `ping` | Tests end-to-end IP reachability to a remote host using ICMP Echo requests.<br><br>**When to use in DevOps:** Diagnostic sanity check to verify if a newly provisioned server, VM, or container host is alive on the network before attempting SSH or deployments. | # Ping a server 4 times and stop automatically:<br>`ping -c 4 google.com` |
| **Path Analysis** | `traceroute` / `mtr` | Traces network path/hops taken by IP packets to reach a destination.<br><br>**When to use in DevOps:** Debugging high-latency alerts, routing drops, or VPN/DirectConnect bottlenecks to pinpoint exactly which network hop or ISP is failing. | # Trace network path to a domain:<br>`traceroute youtube.com`<br># Interactive real-time trace:<br>`mtr youtube.com` |
| **Interface Status** | `ifconfig` / `ip address show` | Configures and displays local interface IP details and hardware metrics.<br><br>**When to use in DevOps:** Auditing internal/external IP bindings on CI/CD runners, Kubernetes nodes, or EC2 instances to configure binding addresses for applications. | # Show all network interfaces and assigned IPs:<br>`ip address show`<br>*(or `ip a` / `ifconfig`)* |
| **Interface Status** | `ifplugstatus` | Checks physical or wireless link connection status (link beat) on local interfaces.<br><br>**When to use in DevOps:** Troubleshooting physical on-premise hardware, bare-metal servers, or local lab environment interface connectivity. | # Check link status across all interfaces:<br>`ifplugstatus` |
| **Wireless** | `iwconfig` | Displays and configures wireless network parameters (SSID, frequency, bit rate).<br><br>**When to use in DevOps:** Rarely used on production cloud servers; useful when configuring or troubleshooting local IoT edge devices, gateway devices, or developer Wi-Fi hardware. | # View details for wireless card:<br>`iwconfig wlp7s0` |
| **Socket Stats** | `netstat` / `ss` | Shows active network sockets, listening ports, routing tables, and interface statistics.<br><br>**When to use in DevOps:** Troubleshooting "address already in use" deployment errors, identifying which PID is holding a port open, or verifying reverse proxies (e.g., Nginx). | # Show listening TCP/UDP ports with PIDs:<br>`ss -tulnp`<br>*(or `netstat -tulnp`)* |
| **System Info** | `hostname` / `cat /etc/hosts` | Displays system host name and static local DNS mapping definitions.<br><br>**When to use in DevOps:** Verifying node identities in automated scripts, or setting local DNS overrides during staging environment testing and microservice development. | # View hostname:<br>`hostname`<br># View static DNS mappings:<br>`cat /etc/hosts` |
| **DNS Resolution** | `dig` | Queries DNS name servers for host addresses, mail exchanges, and record details.<br><br>**When to use in DevOps:** Verifying DNS propagation after updating Route53 records, testing custom DNS resolvers, or troubleshooting domain resolution failures. | # Perform DNS lookup for A records:<br>`dig youtube.com` |
| **DNS Resolution** | `whois` | Queries domain registration databases for ownership, domain registrar, and expiration details.<br><br>**When to use in DevOps:** Auditing domain expiration dates, identifying domain registrars, or verifying domain ownership/NS records during domain migrations. | # Query domain registration records:<br>`whois youtube.com` |
| **LAN Inspection** | `arp` | Displays and modifies the local ARP cache table mapping IPv4 addresses to MAC addresses.<br><br>**When to use in DevOps:** Troubleshooting local network communication issues, IP conflicts, or gateway reachability on on-premise networks or bare-metal clusters. | # Display local ARP cache:<br>`arp` |
| **Network Routing** | `route` / `ip route` | Displays or modifies the kernel's IP routing table.<br><br>**When to use in DevOps:** Diagnosing asymmetric routing issues, checking VPN routes, or confirming container interface routing paths (Docker/Kubernetes). | # View current kernel routing table:<br>`route`<br>*(or `ip route`)* |
| **Port Scanning** | `nmap` | Discovers open ports, running services, and security parameters on host targets.<br><br>**When to use in DevOps:** Performing security audits, verifying AWS Security Group rules, or testing whether specific application ports are exposed to the public internet. | # Scan host for open web ports and services:<br>`nmap -v youtube.com` |
| **Web Requests** | `curl` | Transfers data to or from a server using protocols such as HTTP, HTTPS, or FTP.<br><br>**When to use in DevOps:** Testing REST API endpoints, verifying HTTP status response codes, writing health check scripts, or testing ingress controllers. | # Send GET request to REST API:<br>`curl -X GET https://dummy.restapiexample.com/api/v1/employees` |
| **JSON Processing** | `jq` | Command-line JSON processor used to slice, filter, transform, and format JSON data.<br><br>**When to use in DevOps:** Parsing structured API responses in shell scripts, filtering AWS CLI JSON output, or validating Kubernetes/Docker JSON configs. | # Pretty-print formatted JSON response:<br>`curl -s <API_URL> \| jq` |
| **File Transfer** | `wget` | Non-interactive command-line tool for downloading files from the web via HTTP, HTTPS, or FTP.<br><br>**When to use in DevOps:** Downloading installation scripts, binary releases, or remote assets directly onto cloud instances inside CI/CD pipelines. | # Download file directly from URL:<br>`wget https://example.com/file.tar.gz` |
| **Socket Connection** | `netcat` / `nc` | Reads and writes data across network connections over TCP or UDP.<br><br>**When to use in DevOps:** Rapidly testing TCP port connectivity to remote services (e.g., databases, Redis) when full client tools are unavailable. | # Check if a specific TCP port is open:<br>`nc -zv youtube.com 80` |
| **Firewall Management** | `iptables` | Configures IPv4 packet filtering rules, NAT, and packet mangling in the Linux kernel.<br><br>**When to use in DevOps:** Auditing host-level firewall rules, setting up port forwarding, or debugging Docker network isolation rules. | # List active firewall rules with detailed packet counts:<br>`sudo iptables -L -v -n` |

---

## 1. Domain Name System (DNS) & Domain Lookup

### `dig` (Domain Information Groper)
Used to query DNS name servers for information about host addresses, mail exchanges, name servers, and related information.

* **Usage:** `dig <domain-name>`
* **Key Observations:**
  * Displays the **A Record** (IPv4 addresses) associated with the target domain.
  * Shows local resolver info under `SERVER:` (e.g., systemd-resolved local interface `127.0.0.53#53`).
  * Displays query response time and DNS record TTL (Time To Live).

### `whois`
Queries regional Internet registries (RIR) to retrieve administrative, technical, ownership, and registration details for a given domain name or IP address block.

* **Usage:** `whois <domain-name>`

---

## 2. Local Area Network (LAN) & Interface Utilities

### `arp` (Address Resolution Protocol)
Displays and modifies the local ARP cache table, which maps IPv4 addresses to local hardware (MAC) addresses (`ether`).

* **Usage:** `arp`
* **Output Analysis:**
  * Maps IP endpoints (e.g., local gateway `reliance.reliance` / `192.168.29.20`) to their physical network card MAC address on a specific network interface (`wlp7s0`).

### `ifplugstatus`
Checks the physical link detection status (link beat) on local network interface controllers.

* **Usage:** `ifplugstatus`
* **Status Types:**
  * `link beat detected`: Physical or wireless interface active/connected (e.g., `lo`, `wlp7s0`).
  * `unplugged`: Interface inactive or disconnected (e.g., `enp6s0`, `docker0`).

---

## 3. Network Routing & Inspection

### `route` / `ip route`
Displays or modifies the IP routing table configured on the operating system kernel.

* **Usage:** `route` (or modern equivalent: `ip route`)
* **Output Breakdown:**
  * `default`: Points traffic destined outside local subnets toward the default gateway router on `wlp7s0`.
  * **Local subnets:** (e.g., `192.168.29.0/24` or Docker bridge `172.17.0.0/16`) route directly through their designated local interfaces without extra network hops.

---

## 4. Port Scanning & Reconnaissance

### `nmap` (Network Mapper)
A security scanner used to discover hosts, open TCP/UDP ports, running services, and OS details on a remote host.

* **Usage Practiced:** `nmap -v youtube.com`
* **Output Analysis:**
  * Automatically scans top 1000 standard ports on target host IP.
  * Found open web ports:
    * `80/tcp` (HTTP)
    * `443/tcp` (HTTPS)
  * Uncovered reverse DNS (rDNS) hostnames associated with target IP addresses (e.g., `lcbome-in-f93.1e100.net`).

---

## 5. Web Requests, Data Fetching & JSON Parsing

### `curl`
A tool for transferring data to or from a server using various protocols (HTTP, HTTPS, FTP, etc.).

* **Usage:** `curl -X GET <URL>`
* **Example:**
```bash
  curl -X GET [https://dummy.restapiexample.com/api/v1/employees](https://dummy.restapiexample.com/api/v1/employees)
```

### `jq` (Command-Line JSON Processor)
Pipes raw text JSON input into structured, color-coded formatting.

* **Usage with Pipe**: curl -X GET <URL> | jq

* **Troubleshooting Note**:
If curl outputs HTML error pages or incomplete API payloads (e.g., HTTP 429 rate limits or cloud protection blocks), jq throws a parse error: Invalid numeric literal because it expected valid JSON structure. Retrying or requesting clean REST endpoints successfully prints formatted objects.

### `wget`
Non-interactive network downloader capable of downloading files via HTTP, HTTPS, and FTP over background sessions.

* **Usage**: wget <URL>

---

## 6. Connectivity, Socket Utilities & Firewalls

### `netcat / nc`
Known as the "Swiss Army knife" of networking; used for reading/writing data across network connections via TCP or UDP.

* **Syntax Note**: Requires specifying both a target address and a destination port.
* **Incorrect**: netcat 80 (throws missing port number)
* **Correct**: nc -zv <hostname/IP> <port> (e.g., nc -zv youtube.com 80)

### `iptables`
Administration tool for IPv4 packet filtering, NAT rules, and network firewall configurations built into the Linux kernel.

* **Usage**: `sudo iptables -L -v -n` (lists active packet filter chains and rules)


## Other networking commands


| Tool Category | Command | Description | Example |
| :--- | :--- | :--- | :--- |
| **Connectivity** | `ping` | Tests end-to-end IP reachability to a remote host using ICMP Echo requests.<br><br>**When to use in DevOps:** Diagnostic sanity check to verify if a newly provisioned server, VM, or container host is alive on the network before attempting SSH or deployments. | # Ping a server 4 times and stop automatically:<br>`ping -c 4 google.com` |
| **Path Analysis** | `traceroute` / `mtr` | Traces network path/hops taken by IP packets to reach a destination.<br><br>**When to use in DevOps:** Debugging high-latency alerts, routing drops, or VPN/DirectConnect bottlenecks to pinpoint exactly which network hop or ISP is failing. | # Trace network path to a domain:<br>`traceroute google.com`<br># Interactive real-time trace:<br>`mtr google.com` |
| **Interface Status** | `ifconfig` / `ip address show` | Configures and displays local interface IP details and hardware metrics.<br><br>**When to use in DevOps:** Auditing internal/external IP bindings on CI/CD runners, Kubernetes nodes, or EC2 instances to configure binding addresses for applications. | # Show all network interfaces and assigned IPs:<br>`ip address show`<br>*(or `ip a` / `ifconfig`)* |
| **Wireless** | `iwconfig` | Displays and configures wireless network parameters (SSID, frequency, bit rate).<br><br>**When to use in DevOps:** Rarely used on production cloud servers; useful when configuring or troubleshooting local IoT edge devices, gateway devices, or developer Wi-Fi hardware. | # View details for wireless card:<br>`iwconfig wlp7s0` |
| **Socket Stats** | `netstat` / `ss` | Shows active network sockets, listening ports, routing tables, and interface statistics.<br><br>**When to use in DevOps:** Troubleshooting "address already in use" deployment errors, identifying which PID is holding a port open, or verifying reverse proxies (e.g., Nginx). | # Show listening TCP/UDP ports with PIDs:<br>`ss -tulnp`<br>*(or `netstat -tulnp`)* |
| **System Info** | `hostname` / `cat /etc/hosts` | Displays system host name and static local DNS mapping definitions.<br><br>**When to use in DevOps:** Verifying node identities in automated scripts, or setting local DNS overrides during staging environment testing and microservice development. | # View hostname:<br>`hostname`<br># View static DNS mappings:<br>`cat /etc/hosts` |