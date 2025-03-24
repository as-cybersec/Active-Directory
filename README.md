# Active-Directory Lab

This document presents a detailed account of the process I followed to establish an Active Directory (AD) home lab, highlighting the steps undertaken, the knowledge gained, and the results achieved. The lab involved configuring a Domain Controller (DC), setting up DHCP and DNS services, and joining a Windows client to the domain. Screenshots are included to provide visual context for each stage of the implementation.


## Overview

Active Directory (AD) is a critical Microsoft technology designed to centralize the management and organization of networks. Through this lab, I obtained hands-on experience in setting up and managing AD components, enhancing my understanding of foundational networking principles and system administration practices.


## Prerequisites

To set up this lab, I ensured the following requirements were met:

Virtualization Platform: I used VirtualBox for creating and managing virtual machines.

Operating System ISOs: Windows Server 2022 and Windows 10 installation files.

System Resources: A host machine with 16 GB of RAM and a multi-core processor.

Networking Knowledge: Familiarity with DHCP, DNS, and NAT networking.


## Lab Environment Setup


### Virtual Network Configuration

I configured a NAT network within VirtualBox to provide internet access and enable seamless communication between virtual machines.

![nat-network](https://github.com/user-attachments/assets/429bf09d-76fb-42f3-89b3-e5520882761a)

### Virtual Machines

I deployed two virtual machines for this lab:

Windows Server: Configured as the Domain Controller.
![dc-config](https://github.com/user-attachments/assets/681e4389-effb-406e-bb29-ca68d1003b35)

Windows 10 Client: Configured as a domain-joined workstation.
![win10-config](https://github.com/user-attachments/assets/c150797a-815b-459f-b572-f44cb72c35bf)

## Configuring the Domain Controller (DC)

### Assigning a Static IP Address

To ensure consistent communication, I assigned a static IP address to the Windows Server.


![dc-static-ip](https://github.com/user-attachments/assets/3a3541aa-6bf4-4ff4-a744-9ab12bad676d)
![dc-static-ip2](https://github.com/user-attachments/assets/2ba5b2b0-763c-4c46-a1dd-62de5c57b34e)

### Renaming the Server

The server was renamed to "cyb-addc-01" to reflect its role as the Domain Controller.
![dc-rename](https://github.com/user-attachments/assets/57e849ae-8695-48a8-bba5-b9a97f6064eb)


### Installing the Active Directory Domain Services (AD DS) Role

I installed the AD DS, DHCP, and DNS roles to enable the server to act as a Domain Controller.

![server-roles](https://github.com/user-attachments/assets/7d8be174-da96-4a0a-b1ac-695d0807fb11)


### Promoting the Server to a Domain Controller

The server was promoted to a Domain Controller, and a new forest named cyberdfir.local was created.

![dc-promote](https://github.com/user-attachments/assets/dc9084f0-6fa5-49dd-b50f-043f8e3f0e6f)
![dc-promote2](https://github.com/user-attachments/assets/299b5ec5-7927-4898-bb08-5a980dc3667d)
![dc-promote3](https://github.com/user-attachments/assets/09c61d54-149e-48ab-ab62-41752291bafe)



## Setting Up DHCP and DNS


### Configuring DHCP

I added and configured the DHCP role on the Domain Controller. An IP scope was defined to allocate IP addresses to client devices.

![ip-scope](https://github.com/user-attachments/assets/524fbd31-adaa-4844-8f73-2531e44e2ef0)

![dhcp-scope](https://github.com/user-attachments/assets/fa1fab8e-5746-4ff7-bc23-cf94c1223760)
![dhcp-config](https://github.com/user-attachments/assets/5966a40b-1d7e-4ee2-b26f-0680ec5c5ce6)


### Verifying DNS Configuration

I verified that forward and reverse lookup zones were properly configured to support domain name resolution.
![rev-lookup](https://github.com/user-attachments/assets/e7a5e32a-9e30-4b4c-99d9-3babc483db32)
![forwarder](https://github.com/user-attachments/assets/41d5791d-7fcb-47fb-be1d-94050b33cfef)


## Joining a Windows Client to the Domain


### Preparing the Client

I renamed the Windows 10 machine to improve identification within the network.

![pc-rename](https://github.com/user-attachments/assets/f3a965ca-0947-4486-a981-68c79cc78eaa)


### Domain Join Process

The Windows 10 client was successfully joined to the mydomain.local domain.

![domain-join](https://github.com/user-attachments/assets/f0b91aeb-c075-47f5-ab75-8928ed2c3064)


### Verifying DHCP Functionality

The client obtained an IP address from the DHCP server, confirming successful configuration.
![client-dhcp-success](https://github.com/user-attachments/assets/a639b6a7-1092-4a7b-945b-8f098e754e90)


## Group Policy and User Management


### Creating Organizational Units (OUs)

To streamline administration, I created Organizational Units (OUs) and organized users and groups accordingly.
![ou-groups-users](https://github.com/user-attachments/assets/7def6f29-a6e9-4ea2-a2e6-62a753953f6b)
![ou-groups-users2](https://github.com/user-attachments/assets/ff27cf51-c491-48f3-b9a6-f2eefa1639f7)


### Implementing Group Policies

I enforced security policies by configuring password complexity requirements, account lockout threshold, and an interactive logon message.
![password-policy](https://github.com/user-attachments/assets/750db259-108e-45cb-9622-7b545fc117e7)
![acct-lockout](https://github.com/user-attachments/assets/4c0e39ce-0d5b-4103-9f9f-b66fab0514ca)
![gpo-logon-policy](https://github.com/user-attachments/assets/60f5a7e3-c044-4e8b-913f-e3dab5d1a4f3)



### Testing and Validation


## DNS Resolution Testing

I verified proper DNS name resolution within the domain environment.
![dns-resolution](https://github.com/user-attachments/assets/dfac1da4-4700-411b-ba52-ec8c5cad03df)


### Group Policy Validation

I confirmed that Group Policies were applied successfully to the client machine.
![pass-policy](https://github.com/user-attachments/assets/4e0a31a0-e6c0-4aba-b646-fd4d3fad0098)
![gp-complexity](https://github.com/user-attachments/assets/f6fcc629-3536-45a4-9d57-7a621ca3dc3a)


## Conclusion

Completing this lab provided invaluable hands-on experience with Active Directory setup and management. I developed a deeper understanding of AD configuration, DHCP and DNS implementation, and Group Policy enforcement. This foundational knowledge positions me to explore advanced features, such as delegation, auditing, and infrastructure optimization, in future projects.

