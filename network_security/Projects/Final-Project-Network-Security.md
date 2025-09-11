# Network Security Final Project


<p align ="center">
    <img src= "/network_security/photo/NetSec_Final_diagram.png" alt = "cloud deployment"
</p>

## 📌 Overview
This project demonstrates the design and configuration of a secure enterprise network using **Cisco devices**.  
The network implements **subnetting**, **OSPF routing**, and **security best practices** such as **SSH access**, **encrypted and hashed passwords**, and **local authentication**, **RADIUS authentication**, **TACACS+ authentication**. Also **NTP synchronization** and **Centralized Syslog logging**.

---

## 🛠️ Lab Environment
- **16 PCs**
- **9 Routers (ISR 4331)**
  - 2 VPN Routers
  - 6 Core Routers
- **11 Switches**
- **2 Web Servers**
- **1 RADIUS Server**
- **1 TACACS+ Server**
- **1 Syslog Server**
- **1 NTP Server**

---

## 🌐 Network Addressing
- **Main LAN**: `192.168.1.0/24`
- Divided into **17 Subnets**
- **Routing Protocol**: OSPF

---

## 🔒 Security Features
- SSH enabled on all routers and switches
    - Domain name: `saeed.local`
        
    - RSA cryptographic keys
        
    - Local user accounts with **secret passwords**
        
- Disabled insecure access methods (Telnet) in favor of **SSH only**
- `enable secret` configured on every device
- `service password-encryption` enabled
- Console & VTY lines protected with login & password
- AAA Authentication:
    - Local accounts (username saeed secret cisco)
    - RADIUS server authentication
    - TACACS+ server authentication
    - Network services:
    - NTP server for time synchronization
    - Syslog server for centralized log collection

  ---

# Subnet Details

### 🌐 Subnet 1 | `192.168.1.0/28`
- **R1** → `192.168.1.1`  
- **S1** → `192.168.1.2`  
- **PCs** → `192.168.1.3` → `192.168.1.8`  



### 🌐 Subnet 2 | `192.168.1.16/28`
- **R2** → `192.168.1.17`  
- **S2** → `192.168.1.18`  
- **S3** → `192.168.1.19`  
- **S4** → `192.168.1.20`  
- **PCs** → `192.168.1.21 - 192.168.1.22`  



### 🌐 Subnet 3 | `192.168.1.32/29`
- **R3** → `192.168.1.33`  
- **S5** → `192.168.1.34`  
- **PC** → `192.168.1.35`  
- **TACACS+ Server** → `192.168.1.36`  
- **RADIUS Server** → `192.168.1.37`  



### 🌐 Subnet 4 | `192.168.1.40/29`
- **R3 (int g0/0/1)** → `192.168.1.41`  
- **S6** → `192.168.1.42`  
- **NTP Server** → `192.168.1.43`  
- **Syslog Server** → `192.168.1.44`  



### 🌐 Subnet 5 | `192.168.1.48/29` *(DMZ)*
- **R4** → `192.168.1.49`  
- **S7** → `192.168.1.50`  
- **PC** → `192.168.1.51`  
- **Web Server** → `192.168.1.52`  



### 🌐 Subnet 6 | `192.168.1.56/29` *(Inside Zone)*
- **R4 (int g0/0/1)** → `192.168.1.57`  
- **S8** → `192.168.1.58`  
- **PCs** → `192.168.1.59 - 192.168.1.60`  



### 🌐 Subnet 7 | `192.168.1.64/29`
- **R5** → `192.168.1.65`  
- **S9** → `192.168.1.66`  
- **PCs** → `192.168.1.67 - 192.168.1.68`  



### 🌐 Subnet 8 | `192.168.1.72/29`
- **R6** → `192.168.1.73`  
- **S10** → `192.168.1.74`  
- **PC** → `192.168.1.75`  
- **Web Server 2** → `192.168.1.76`  



### 🌐 Subnet 9 | `192.168.1.80/29` *(Test Network)*
- **R7** → `192.168.1.81`  
- **S11** → `192.168.1.82`  
- **PC** → `192.168.1.83`  



### 🌐 Subnet 10 → Subnet 17
- **WAN links (Point-to-Point)** between routers  
- Using `/30` networks ranging from:  
  - `192.168.1.88/30` → `192.168.1.116/30`

----
### Lab Env
- PC: 16
- Router ISR 4331: 9 (2 VPN Routers, 6 Routers)
- Switch ISR : 11
- WEB Server: 2
- RADIUS Server: 1
- TACACS + Server: 1
- Syslog Server: 1
- NTP Server: 1
- Lan **`192.168.1.0/24`**

----

## Sample Configuration

### Subnet 1 | 192.168.1.0/28 R1
#### R1 Conf
```
en
conf t
hostname R1
int gig0/0/0 
ip address 192.168.1.1 255.255.255.240
no shut down
ex

enable secret cisco
line console 0
password cisco
login
exit

service password-encryption


ip domain-name saeed.local
crypto key generate rsa
1024

username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit

router ospf 1
network 192.168.1.0 0.0.0.15 area 0
```

#### S1 Conf
```
en
conf t
hostname S1
int vlan 1
ip address 192.168.1.2 255.255.255.240
no shut down
ex
ip default-gateway 192.168.1.1

enable secret cisco
line console 0
password cisco
login
exit

service password-encryption


ip domain-name saeed.local
crypto key generate rsa
1024

username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit

```

#### PCs Con
PCs: `192.168.1.3` <-> `192.168.1.8`

---
## Need More Details?
This README contains the project overview, subnet plan, and sample configurations.  
If you would like the **full configuration files and additional documentation**, feel free to contact me on **[LinkedIn](https://www.linkedin.com/in/saeed-elfiky-61188b24b/)**.  


  
