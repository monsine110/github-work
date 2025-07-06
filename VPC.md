
---

# 🌐 **Mastering Cloud Networking with AWS**  
### *A Hands-On Guide to IP Addressing,DHCP,DNS,NAT AND VPC design 
## 🧭 **Overview**
In today's cloud-native landscape, mastering the design and configuration of secure, scalable networks in AWS is essential for developers, DevOps engineers, and architects. This guide walks you through building a layered AWS VPC architecture—featuring public and private subnets, NAT gateways, VPC peering—and expands into critical network concepts such as DNS, NAT types, DHCP, and CIDR.

---

---

## 🛡️ **Part 1: Understanding Network Components**

### ✅ Virtual Private Cloud (VPC)
- Isolated, customizable network environment inside AWS
- Allows segmentation with subnets and robust control via route tables and security groups

### ✅ DNS Servers
- Translate domain names into IP addresses
- Includes Recursive, Root, TLD, Authoritative, Caching, and Forwarding DNS types

### ✅ NAT (Network Address Translation)
- Enables private subnet access to external networks
- 🔄 **Types of NAT**:
  - Static
  - Dynamic
  - PAT (Port Address Translation)
  - NAT64
  - Bidirectional NAT

### ✅ DHCP (Dynamic Host Configuration Protocol)
- Automatically assigns IP addresses and networking info to clients
- Key benefit: reduces manual errors, reuses IPs efficiently, simplifies network setup

### ✅ CIDR (Classless Inter-Domain Routing)
- CIDR notation (e.g. `192.168.1.0/24`) helps flexibly define networks
- Allows subnetting and route summarization for more efficient IP use

🧮 Example:
```
Given 172.16.130.0/24 → 32 - 24 = 8 bits for hosts
2^8 = 256 addresses → 254 usable (excluding network and broadcast)
```

---
---

## 📦 **Part 2: Designing a Secure AWS VPC**

### 🔹 What You'll Learn:
- Creating a custom VPC from scratch
- Setting up public and private subnets with proper routing
- Launching EC2 instances with internet access control
- Configuring NAT for outbound access and subnet isolation
- Building VPC peering between isolated cloud environments

🛠️ Includes: Screenshots, subnet CIDRs, routing diagrams, and security best practices.

---

## 🔗 **Part 3: Inter-VPC Communication with VPC Peering**

- Enable private communication between isolated VPCs
- Step-by-step: Create peering connection, accept it, update route tables, test with ping or SSH
- 🔐 Adjust security groups to allow cross-VPC traffic

🎯 Use case: Connecting apps across environments, microservice communication, hybrid cloud setups

---

## 🧠 **Conclusion: Cloud Networking Done Right**

This guide equips you with practical knowledge to:
- Architect multi-tier VPCs with granular access control
- Secure internal systems with subnet segmentation and NAT
- Understand foundational internet protocols underpinning cloud networking

Whether you're setting up a production-ready AWS environment or studying for certification, you now have a structured blueprint to reference and build from.

---
---
# PART 1
---
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


# **Network Address Translation (NAT)** .
 this is a technique used in networking to modify IP addresses in data packets as they pass through a router or firewall. It allows multiple devices on a private network to share a single public IP address when accessing the internet.

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

---
# PART 2
---
# Building a Secure AWS VPC with Public and Private Subnets, Instances, and a NAT Gateway #
Creating a well-architected network infrastructure in AWS starts with a Virtual Private Cloud (VPC). By dividing the VPC into public and private subnets and setting up a NAT gateway, you ensure both internet accessibility and secure backend communication for your applications.  
![alt text](./screenshot/Screenshot%202025-06-27%20142309.png)
Here’s how to build one from scartch
1. Create Your VPC
Start by creating a VPC to isolate your cloud network resources.
- Step: Open the AWS VPC Console → Select "Create VPC"
- Configuration:
- Name: my-vpc
- IPv4 CIDR block: 172.16.0.0/16
- Tenancy: Default
- Result: This provides your own private network space in the cloud.
![alt text](./screenshot/Screenshot%202025-06-27%20153936.png)
2. Set Up Subnets
Split your network into zones: public (internet-facing) and private (backend/data services).
- ## Public Subnet
- CIDR Block: 172.16.1.0/26
- Availability Zone: Choose based on region
- Used for: EC2 instances that need internet access
![alt text](./screenshot/Screenshot%202025-06-27%20154444.png)
![alt text](./screenshot/Screenshot%202025-06-27%20154510.png) 
- ##  Private Subnet
- CIDR Block: 172.16.2.0/26
- Used for: Internal-only resources like databases
![alt text](./screenshot/Screenshot%202025-06-27%20154934.png)
3. internet gateway 
- create internet gateway
![alt text](./screenshot/Screenshot%202025-06-27%20155111.png)
- attach it to the vpc
![alt text](./screenshot/Screenshot%202025-06-27%20155205.png)
![alt text](./screenshot/Screenshot%202025-06-27%20155224.png)
4. create route tables
- when creating a subnet a route table was create
so we name it public table and create a private route table attach it to the vpc
![alt text](./screenshot/Screenshot%202025-06-27%20155421.png)
- associate public routable to the public subnet
![alt text](./screenshot/Screenshot%202025-06-27%20155549.png)
- associate the private route table to the private subnet
![alt text](./screenshot/Screenshot%202025-06-27%20155624.png)



4. Launch EC2 Instances: Deploy servers within each subnet.
- Public Subnet Instance:
    - Launch a standard EC2 instance
    - Associate with the public subnet
    - Attach a public IP
    - Attach a security group allowing SSH access
![alt text](./screenshot/Screenshot%202025-06-27%20161638.png)
![alt text](./screenshot/Screenshot%202025-06-27%20161935.png)
- Private Subnet Instance:
    - Launch another EC2 instance
    - Place it inside the private subnet
    - No public IP (accessible only via the NAT gateway or bastion host)
    ![alt text](./screenshot/Screenshot%202025-06-27%20162733.png)
    ![alt text](./screenshot/Screenshot%202025-06-27%20162821.png)

5.    Accessing EC2 Instances with MobaXterm

 . Prepare Your Key Pair
    - When you launched your EC2 instance, AWS provided a .pem private key.
. Launch a New SSH Session
    - Open MobaXterm → Click Session → Choose SSH
    - In the session settings:
    - Remote host: Public IP of your EC2 instance
        - Specify username
    - Use private key: Navigate to and select your .pem file
    ![alt text](./screenshot/Screenshot%202025-06-27%20163449.png)
. Configure Network Access 
    - Make sure your security group allows inbound SSH (port 22) from your IP address.
![alt text](./screenshot/Screenshot%202025-06-27%20163608.png)


6. Create and Attach a NAT Gateway
Private instances need outbound internet access (e.g., to install packages). A NAT gateway handles this securely.
- Step: Go to NAT Gateways → Click "Create NAT Gateway"
- Subnet: Place it in the public subnet
- Elastic IP: Allocate and associate one
![alt text](./screenshot/Screenshot%202025-06-27%20164912.png)
- Attach to Routing:
- Update the private subnet’s route table
- Add a route: 0.0.0.0/0 → Target the NAT gateway
. Configure Route Tables
Ensure traffic flows correctly between your VPC components.
- Public Route Table:
- Route: 0.0.0.0/0 → Internet Gateway
- Private Route Table:
- Route: 0.0.0.0/0 → NAT Gateway
## SSH from Bastion to Private Server
### Connect to Bastion Host
- From your local machine via MobaXterm 


### Make Sure the Key is on the Bastion
- If your private key (.pem) is not already on the bastion, edit the .pem file using notepad copy the key and create a file on the bastion using vim editor, paste your key and save and quit 
- On the bastion, set permissions:
chmod 600 your-key.pem

### SSH into the Private Instance
- From the bastion:
ssh -i your-key.pem ec2-user@<private-instance-ip>
![alt text](./screenshot/Screenshot%202025-06-27%20164720.png)
 Make sure the security group of the private server allows SSH from the internal IP of the bastion, not just anywhere.

With this setup, your architecture balances accessibility and security. The public subnet handles frontend traffic while the private subnet—with help from the NAT gateway—securely supports backend operations like databases or internal services. This model is the backbone of scalable, secure cloud infrastructure.





Certainly, Newlife! Based on the architecture in your diagram, here’s a comprehensive article that explains how to build a structured and secure network in AWS—with public and private subnets, a NAT Gateway, and specific routing rules that exclude one private subnet from external internet access.

---

# **Creating an AWS VPC with Public and Three Private Subnets (One Without Internet Access)**
![alt text](./screenshot/Screenshot%202025-06-28%20165537.png )

Cloud-native architectures prioritize control, scalability, and security. In this guide, you’ll learn how to create an AWS Virtual Private Cloud (VPC) that includes:

- One public subnet
- Three private subnets, with only two of them having internet access via a NAT Gateway
- EC2 instances across all subnets
- A secure and structured route configuration

---

## 1. **Create a VPC**

1. Go to the **VPC Dashboard** in AWS
2. Click **Create VPC**, choose “VPC only”
   - Name: `test-vpc`
   - CIDR block: `172.16.0.0/16`
   - Tenancy: Default

Click **Create**.
![alt text](./screenshot/Screenshot%202025-06-28%20180814.png)
---

## 2. **Create Subnets**

Use these ranges, as illustrated in your architecture:

| Subnet Name         | Type     | CIDR Block       |
|---------------------|----------|------------------|
| PublicSubnet        | Public   | `172.16.1.0/26`  |
| PrivateSubnet-A     | Private  | `172.16.2.0/26`  |
| PrivateSubnet-B     | Private  | `172.16.3.0/26`  |
| PrivateSubnet-C     | Private  | `172.16.4.0/26`  |

For each, specify the **Availability Zone** (e.g., `us-east-1a`) for high availability and redundancy.

---
![alt text](./screenshot/Screenshot%202025-06-28%20181307.png)
![alt text](./screenshot/Screenshot%202025-06-28%20181419.png )
![alt text](./screenshot/Screenshot%202025-06-28%20181616.png)
![alt text](./screenshot/Screenshot%202025-06-28%20181845.png)
![alt text](./screenshot/Screenshot%202025-06-28%20181902.png)

## 3. **Set Up the Internet Gateway (IGW)**

1. Go to **Internet Gateways** > Create IGW → attach it to your VPC
![alt text](./screenshot/Screenshot%202025-06-28%20182412.png)
![alt text](./screenshot/Screenshot%202025-06-28%20182507.png)
2. rename the **route table** that was automatically created when you created the subnet and associate it with the public subnet:
![alt text](./screenshot/Screenshot%202025-06-28%20183131-1.png)
- Edit the **route table** 
   - Add route: `0.0.0.0/0` → target the **Internet Gateway**
   ![alt text](./screenshot/Screenshot%202025-06-28%20183511.png)

This gives the public subnet internet access.




## 4. **Provision a NAT Gateway**

To provide internet access to **only** PrivateSubnet-A and PrivateSubnet-B:

1. Allocate an Elastic IP in AWS
2. Go to **NAT Gateways** and create
   - Name: `test-vpc-nat`
   - Subnet: **PublicSubnet**
   - Elastic IP: Associate your allocated IP
   ![alt text](./screenshot/Screenshot%202025-06-28%20183725.png)
3. Create a route table named `PrivateRouteTable`:
   - Add route: `0.0.0.0/0` → target the NAT Gateway
   - Associate it with **PrivateSubnet-A** and **PrivateSubnet-B**
![alt text](./screenshot/Screenshot%202025-06-28%20182944-1.png)
![alt text](./screenshot/Screenshot%202025-06-28%20184252.png)
![alt text](./screenshot/Screenshot%202025-06-28%20183856.png)
>  **Do NOT associate this route table with PrivateSubnet-C.** That subnet will remain isolated from outbound internet traffic for enhanced security (e.g., for sensitive databases).

---

## 5. **Launch EC2 Instances**

Launch instances into each subnet with the following considerations:

- **Public Subnet:**
  - Instance with public IP (e.g., for SSH access or as a bastion)
  - Security group allows SSH (port 22) from your IP

- **Private Subnets A & B:**
  - Application EC2s
  - No public IPs
  - Security groups allow traffic from public subnet (if needed)

- **Private Subnet C:**
  - EC2 instance 
  - Isolated (no route to NAT Gateway, no public IP)
![alt text](./screenshot/Screenshot%202025-06-28%20185014.png)
![alt text](./screenshot/Screenshot%202025-06-28%20185211.png)
![alt text](./screenshot/Screenshot%202025-06-28%20185447.png)
---

##  6. **Security Configuration**

- Use **Security Groups** to restrict traffic:
  - Public instance allows inbound SSH from your IP only
  - Private instances allow traffic only from the bastion or specific sources
- Use **Network ACLs** optionally to add subnet-level filtering
- Consider adding **CloudWatch Logs** and **VPC Flow Logs** for monitoring

---

## 7. **Why Exclude One Private Subnet from the Internet?**

Leaving **PrivateSubnet-C** without NAT or internet access is a best practice when:

- Hosting **sensitive data** or **databases** that should never reach external networks
- You want to enforce **strict egress isolation**
- Applications in this subnet only talk to internal resources 

---

## **Conclusion**

This VPC design offers flexibility and robust security:

- Public subnet enables internet connectivity and management access
- Private subnets A and B gain outbound internet via NAT for updates and external APIs
- Private subnet C is fully isolated, perfect for high-security applications



---
---

# PART 3
---
# **Connecting VPCs with AWS VPC Peering: A Practical Walkthrough**

Modern cloud infrastructure often requires secure communication between isolated environments. Whether you're linking microservices, databases, or monitoring stacks across two Virtual Private Clouds (VPCs), **VPC Peering** provides a powerful way to bridge networks in AWS.

This guide walks through creating VPC peering between two networks as depicted in the shared architecture.
![alt text](./screenshot/Screenshot%202025-07-02%20160617.png)

---

##  1. **Architecture Summary**

You're creating and  connecting two VPCs:

- **VPC A** with
  - CIDR Block: `172.16.0.0/16`
  - Contains:
    - Public Subnet `172.16.1.0/26`
    - Private Subnet `172.16.2.0/26`
    - EC2 instances with SSH access
    ![alt text](./screenshot/Screenshot%202025-07-03%20154212-1.png)
  
    ![alt text](./screenshot/Screenshot%202025-07-03%20155539.png)
    ![alt text](./screenshot/Screenshot%202025-07-03%20155605.png)

- **VPC B** in another region with
  - CIDR Block: `172.25.0.0/16`
  - Contains:
    - Private Subnet `172.25.1.0/26`
    - EC2 instances communicating with VPC A via ssh
    ![alt text](./screenshot/Screenshot%202025-07-03%20154538.png)
    ![alt text](./screenshot/Screenshot%202025-07-03%20160135.png)
    
    
- **Create an internate gate way and attach to the two vpc's**
![alt text](./screenshot/Screenshot%202025-07-03%20161044.png)

The goal: Enable **bi-directional private communication** using ping or SSH between instances in both VPCs.

---

## 🔧 2. **Create VPC Peering Connection**

###  **Step 1: Initiate Peering**

1. Navigate to **VPC Dashboard → Peering Connections → Create Peering Connection**
2. **Requester VPC:** Select VPC A (`172.16.0.0/16`)
3. **Accepter VPC:**
   - If in the same account: Choose VPC B directly
   - If in a different account: Provide Account ID and VPC ID of VPC B
4. Give the peering connection a tag like `VPC-A-to-VPC-B`
5. Click **Create Peering Connection**
![alt text](./screenshot/Screenshot%202025-07-03%20163409.png)

###  **Step 2: Accept Peering Request**

1. Switch to VPC B’s account or region
2. Go to **Peering Connections**, locate the pending request
3. Click **Actions → Accept Request**
![alt text](./screenshot/Screenshot%202025-07-03%20163532.png)

The connection should now show as **Active**

---

## 📡 3. **Configure Routing**

To ensure traffic flows between VPCs:

###  **VPC A Route Table**

1. Go to **Route Tables** → Select the one attached to  `172.16.2.0/26`
2. Add route:
   - **Destination:** `172.25.0.0/16`
   - **Target:** VPC Peering connection ID
   ![alt text](./screenshot/Screenshot%202025-07-03%20170239-1.png)

### **VPC B Route Table**

1. Select the route table associated with `172.25.1.0/26`
2. Add route:
   - **Destination:** `172.16.0.0/16`
   - **Target:** VPC Peering connection ID
![alt text](./screenshot/Screenshot%202025-07-03%20170358.png)
---

## 4. **Adjust Security Groups**

Make sure instances allow communication:

- **VPC A Instances:**
  - Add an inbound rule to allow traffic from `172.25.0.0/16` (VPC B CIDR)
  ![alt text](./screenshot/Screenshot%202025-07-03%20165552-1.png)
- **VPC B Instances:**
  - Add an inbound rule to allow traffic from `172.16.0.0/16` (VPC A CIDR)
![alt text](./screenshot/Screenshot%202025-07-03%20165552.png) 
If using **SSH**, allow port **22**; for **ping**, allow **ICMP**.

---

## ✅ 5. **Test the Connection**
- ssh into the bastion
![alt text](./screenshot/Screenshot%202025-07-03%20165842.png)
![alt text](./screenshot/Screenshot%202025-07-03%20165903.png)
- from the bastion ssh into the instance in the private subnet of vpc A
![alt text](./screenshot/Screenshot%202025-07-03%20171356.png)
![alt text](./screenshot/Screenshot%202025-07-03%20171455.png)
- ping the intance in VPC B (It will ping because of the peering connection)
![alt text](./screenshot/Screenshot%202025-07-03%20171724.png)
---

## . **Note**

- Avoid **CIDR overlap** between peered VPCs
- Remember: **VPC Peering is not transitive**

---

## Conclusion

VPC peering is a lightweight yet powerful method for connecting networks in AWS. With proper routing and security configurations, your EC2 instances across VPCs can communicate seamlessly—perfect for microservice integrations, data aggregation, or multi-tier deployments.

