# Active-Directory Lab

## Introduction

This write-up documents my journey of setting up and exploring an Active Directory (AD) homelab. Through this project, I aimed to gain hands-on experience with AD fundamentals, security concepts, and administrative tasks. By building this lab environment, I enhanced my understanding of key AD features and how they operate in a controlled setting. This foundational work will be expanded upon in future projects to include advanced configurations, integrations, and security-focused simulations.

## Lab Objectives

During this project, I:

- Learned AD fundamentals, including domains, forests, organizational units (OUs), and trusts.
- Practiced user and group management.
- Configured and tested Group Policy Objects (GPOs).
- Improved my skills in configuring DHCP and DNS roles to ensure network services function seamlessly.
- Developed an understanding of how to join client machines to a domain and troubleshoot connectivity issues.


## Environment Setup

### Hardware/Software Requirements

- **Virtualization Software:** VirtualBox
- **Operating Systems:** Windows Server 2022 ISO and Windows 10 ISO (evaluation versions from Microsoft)

### Network Configuration

- **Virtual Network:** NatNetwork (named `cyberdfir`)

## Step-by-Step Lab Setup

### 1. Virtual Environment Setup

I began by installing VirtualBox and creating a virtual network named `cyberdfir` using the NatNetwork configuration.
![NatNetwork-Config](https://github.com/user-attachments/assets/1449ce90-5d29-4fd8-9917-be9501b45956)

### 2. Deploying the Domain Controller

I created a virtual machine (VM) for Windows Server 2022 with the following specifications:

- **RAM:** 4GB
- **Storage:** 50GB (dynamically allocated)
- **Network:** NatNetwork
![WinServ2022-Config](https://github.com/user-attachments/assets/42cfd95c-8495-4c76-b4d1-fa1cc17b96b9)

The VM was named `cyber-addc-01`, and all Windows Updates were applied before rebooting. Next, I:

- Configured a static IP address for the VM:
  - IP Address: 192.168.10.10
  - Subnet Mask: 255.255.255.0
  - Default Gateway: 192.168.10.1
  - Preferred DNS Server: 192.168.10.10 (to act as its own DNS server)
![DC-Static-IP](https://github.com/user-attachments/assets/ba78830b-61ff-4140-b071-30d2fd250553) 

- Installed the Active Directory Domain Services (AD DS), DNS, and DHCP roles via Server Manager.
- Promoted the server to a domain controller and created a new domain named `cyberdfir.local`.
![DC](https://github.com/user-attachments/assets/e5d7241e-56e8-4dd9-b873-3b4dedf823a6)


### 3. Configuring DHCP

I installed the DHCP Server role on the domain controller and configured a new scope for the subnet `192.168.1.0/24` with the following details:

- **Start IP:** 192.168.1.100
- **End IP:** 192.168.1.200
- **Subnet Mask:** 255.255.255.0
- **Default Gateway:** 192.168.1.1
- **DNS Server:** 192.168.1.10
![DHCP-Scope](https://github.com/user-attachments/assets/ecc8233b-2cfa-4e0f-a516-829cafade1c5)

The scope was activated, and the DHCP server was authorized in AD. I tested the setup by setting a client machine to obtain an IP address automatically, ensuring proper configuration.

### 4. Configuring DNS

Using the DNS Manager, I:

- Verified that the Forward Lookup Zone for `cyberdfir.local` was created.
- Added a Reverse Lookup Zone for the subnet `192.168.10.0/24`.
- ![Rev-Lookup-Zone](https://github.com/user-attachments/assets/e23b0485-fe76-4f64-9399-26496463352f)

- Configured Google’s DNS server (8.8.8.8) as a forwarder for external internet connectivity.

I confirmed DNS resolution by successfully pinging the domain name from both the domain controller and a client machine.

### 5. Adding a Client Machine

I created a Windows 10 Pro VM with these specifications:

- **RAM:** 4GB
- **Storage:** 50GB (dynamically allocated)
- **Network:** NatNetwork
![Win10-Client](https://github.com/user-attachments/assets/10dd1388-4dce-416b-903b-9b8e7f185466)

The client machine was renamed `pc1-cyberdfir`, configured to use DHCP for IP assignment, and joined to the domain. All Windows Updates were applied.
![Domain-join](https://github.com/user-attachments/assets/3d698247-2994-46fe-b3e3-69a2e1218c01)

## Active Directory Features Exploration

### Organizational Units (OUs)

I organized the lab environment by creating OUs for logical grouping (e.g., Users, Computers, IT, HR) and moved user and computer objects into their respective OUs.
![OUs](https://github.com/user-attachments/assets/7652eabc-442c-45ef-9cc2-2b12d551e8d0)
![AD-Features](https://github.com/user-attachments/assets/04dd5ce0-fb4d-4b7b-ac43-857dcb4f15b1)


### User and Group Management

I created domain users with varying permissions and established security groups, assigning users to their respective groups.
![User-Groups](https://github.com/user-attachments/assets/0aaa53d9-ccef-4e46-a44f-973a3107267c)


### Group Policy Objects (GPOs)

I created and linked GPOs to enforce policies, such as password complexity and interactive logon messages. These GPOs were tested on domain-joined client machines to ensure they were applied correctly.
![password-policy2](https://github.com/user-attachments/assets/265de1fb-2e29-4453-852e-bc9d4ea4ecaf)
![password policy3](https://github.com/user-attachments/assets/99e32c34-dc8c-492a-ad46-379251c8d7c6)
![gpo-logon-policy](https://github.com/user-attachments/assets/8da41ec7-ba90-40d4-b7cf-c3043983f105)

## Conclusion

Through this homelab project, I gained a deeper understanding of Active Directory concepts and practical skills in configuring and managing a domain environment. This setup served as a strong foundation for further exploration of AD features, security practices, and advanced configurations. I plan to expand this lab to include redundancy, cloud integration, and advanced security simulations in future projects.
