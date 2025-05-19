# CONCEPTS OF VPC's, DNS SERVERS AND IP ADDRESSES
## VPC's
A Virtual Private Cloud (VPC) is a secure, isolated private cloud hosted within a public cloud. It allows users to run applications, store data, and manage resources in a controlled environment while benefiting from the scalability and flexibility of public cloud infrastructure.

## Key Features of a VPC:
- Isolation: A VPC ensures that computing resources are separated from other users in the public cloud.
- Subnets: Divides the network into smaller segments for better organization and security.
- Security: Uses firewalls, access control lists, and encryption to protect data.
- Connectivity: Can connect to on-premises networks via VPNs or direct links.
- Scalability: Easily adjusts resources based on demand.
 ## DNS SERVERS
A DNS server (Domain Name System server) is a crucial component of the internet that translates human-friendly domain names (like www.example.com) into numerical IP addresses (like 192.168.1.1) that computers use to locate and communicate with each other.
## How DNS Servers Work:
- User Request: When you type a website URL into your browser, your device sends a request to a DNS resolver.
- Recursive Query: The resolver checks its cache for the IP address or queries other DNS servers if needed.
- Root & TLD Servers: The request moves through root servers and top-level domain (TLD) servers (like .com, .org) to find the correct authoritative DNS server.
- Final Resolution: The authoritative DNS server provides the IP address, allowing your browser to connect to the website.
DNS servers come in different types, each serving a specific role in the domain name resolution process. Here’s a breakdown:
## TYPES OF DNS SERVERS
### 1. **Recursive DNS Resolver**
   - Acts as an intermediary between users and authoritative DNS servers.
   - Looks up the requested domain name by querying other DNS servers until the correct IP address is found.
   - Commonly operated by ISPs or third-party providers like Google (`8.8.8.8`) or Cloudflare (`1.1.1.1`).

### 2. **Root DNS Server**
   - The first step in the DNS lookup process.
   - Directs requests to the appropriate Top-Level Domain (TLD) server.
   - There are 13 logical root servers globally, managed by organizations like ICANN.

### 3. **Top-Level Domain (TLD) DNS Server**
   - Manages domains under specific extensions like `.com`, `.net`, `.org`, etc.
   - Helps locate authoritative servers for websites with a particular TLD.

### 4. **Authoritative DNS Server**
   - Stores and provides the actual IP address for a domain.
   - Responds with accurate mapping of domain names to their corresponding IPs.
   - Websites can have their own authoritative servers or rely on hosting providers.

### 5. **Forwarding DNS Server**
   - Receives queries and forwards them to another DNS resolver instead of resolving them itself.
   - Often used to enhance security or optimize network performance.

### 6. **Caching DNS Server**
   - Temporarily stores DNS query results to reduce lookup time and network load.
   - Improves efficiency by retrieving cached responses for repeated queries.


 ## IP ADDRESSES
 An IP address (Internet Protocol address) is a unique numerical label assigned to each device connected to a network that uses the Internet Protocol for communication. It acts like a digital home address, allowing devices to send and receive data accurately.
## Key Concepts of IP Addresses:
- IPv4 vs. IPv6: IPv4 uses a 32-bit format (e.g., 192.168.1.1), while IPv6 uses a 128-bit format (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334) to accommodate more devices.(Though it is difficult to migrate to IPV6)
- Public vs. Private IPs: Public IPs are globally unique and used for internet communication, while private IPs are used within local networks.
- Static vs. Dynamic IPs: Static IPs remain constant, while dynamic IPs change periodically, often assigned by ISPs.
- Routing & Identification: IP addresses help route data between devices and identify them on a network.


**Network Address Translation (NAT)** is a technique used in networking to modify IP addresses in data packets as they pass through a router or firewall. It allows multiple devices on a private network to share a single public IP address when accessing the internet.

### **Key Concepts of NAT**
- **IP Address Translation:** NAT converts private IP addresses into public ones, enabling devices to communicate externally.
- **Security & Privacy:** It hides internal network details, making it harder for external threats to directly target devices.
- **Address Conservation:** Helps mitigate IPv4 address exhaustion by allowing multiple devices to use a single public IP.

### **Types of NAT**
Network Address Translation (NAT) comes in different types, each serving a unique purpose in managing IP addresses within a network. Here’s a deeper dive into the main types:

### **1. Static NAT**
- Maps a private IP address to a fixed public IP address.
- Used when a device needs to be consistently accessible from the internet, such as a web server.
- Example: A company hosting a website may use static NAT to ensure its internal server always maps to the same public IP.

### **2. Dynamic NAT**
- Maps multiple private IP addresses to a pool of public IP addresses.
- Unlike static NAT, the mapping is temporary and changes dynamically.
- Useful when a network has a limited number of public IPs but multiple internal devices needing internet access.

### **3. Port Address Translation (PAT) (NAT Overload)**
- Allows multiple devices to share a single public IP by assigning unique port numbers.
- The most common type of NAT used in home and business networks.
- Example: When multiple devices in a household access the internet, PAT ensures they all use the same public IP but different ports.

### **4. NAT64**
- Used in IPv6 networks to allow communication with IPv4 devices.
- Translates IPv6 addresses into IPv4 addresses, enabling compatibility between different IP versions.

### **5. Bidirectional NAT**
- Allows translation in both directions, enabling communication between two different IP address spaces.
- Often used in complex enterprise networks where multiple address schemes coexist.

Each type of NAT plays a crucial role in managing IP addresses efficiently while ensuring security and connectivity.
## CONCEPT OF DHCP
**Dynamic Host Configuration Protocol (DHCP)** is a network protocol that automatically assigns IP addresses and other network settings to devices, allowing them to communicate efficiently without manual configuration.

### **How DHCP Works**
1. **Discovery:** A device (DHCP client) sends a request to find a DHCP server.
2. **Offer:** The DHCP server responds with an available IP address and configuration details.
3. **Request:** The client selects an offered IP and requests confirmation.
4. **Acknowledgment:** The DHCP server confirms the assignment, and the client can now use the IP address.

### **Key Benefits of DHCP**
- **Automates IP Address Assignment:** Reduces manual configuration errors.
- **Efficient Network Management:** Ensures devices receive correct settings like subnet masks, gateways, and DNS servers.
- **IP Address Conservation:** Reuses addresses dynamically, preventing conflicts.

### **DHCP Components**
- **DHCP Server:** Manages and distributes IP addresses.
- **DHCP Client:** Devices requesting IP addresses.
- **DHCP Relay:** Forwards DHCP requests between networks.

Think of DHCP as a hotel check-in system—when a guest arrives, they’re assigned a room (IP address) without needing to manually pick one.
  
  ## CONCEPT OF CIDR NOTATION
**Classless Inter-Domain Routing (CIDR)** is a method of IP address allocation and routing that improves efficiency by allowing flexible subnetting. Instead of using traditional class-based IP addressing, CIDR enables networks to be divided into variable-sized blocks.

### **Key Concepts of CIDR Notation**
- **CIDR Format:** IP addresses are written with a suffix indicating the number of bits used for the network portion (e.g., `192.168.1.0/24` means the first 24 bits define the network).
- **Subnet Masking:** Subnet masking is the process of applying a subnet mask to an IP address to define the network and host portions. Essentially, it helps a device determine whether another IP address is part of the same local network or needs to be routed externally.
 CIDR replaces fixed subnet masks with variable-length subnet masks (VLSM), allowing more precise allocation of IP addresses.
- **Efficient Routing:** CIDR helps reduce the size of routing tables by aggregating multiple IP addresses into a single entry.
- **Subnetting:** this is the process of dividing large nework into smaller network 


CIDR This was a more flexible way to divide networksinto subnets of any sizeand we do itusing a subnet mask

CIDR notaion is basically IP address/subnet mask  
### HOW TO CALCULATE NUMBER OF IP ADDRESS USING SUBNET MASK 
E.g  172.16.130.0/24     
172.16.130.0 is the IP address while 24 is the subnet mask.   
 24 tells us how many bits are fixed for the network, this means out of 32bits, 
 
 24 has been reserved for the network while the rest is for the host  
 32-24= 8bits
 2^8 =256 IP addresses that are available 

 which are 172.16.130.0, 172.16.130.1, 172.16.130.2...172.16.130.255  
 out of 256 only 254 are usable 
 because  
   172.16.130.0 is called network address
 it is the address that is used to identify the network
 while
  172.16.130.255 is the broadcast address i.e any message sent to the address will be seen the device in the sub network 
 
 

### **Example of CIDR Notation**
- `192.168.1.0/24` → Network: `192.168.1.0`, Host Range: `192.168.1.1` to `192.168.1.255`
- `10.0.0.0/16` → Network: `10.0.0.0`, Host Range: `10.0.0.1` to `10.0.255.255`

CIDR is widely used in modern networking to optimize IP address usage and improve routing efficiency.
