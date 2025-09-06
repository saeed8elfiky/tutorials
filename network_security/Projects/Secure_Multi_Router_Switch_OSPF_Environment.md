# Secure Multi-Router & Switch OSPF Environment

<p align ="center">
    <img src= "/network_security/photo/network_diagram.png" alt = "access management"
</p>


This project is a **Network Security Lab** built with **Cisco ISR 4331 routers** and **ISR switches**.
The goal is not only to configure a functional multi-subnet environment with **OSPF routing**, but also to **secure the infrastructure** against unauthorized access.

---
### Lab Env
- PC: 9
- Router ISR 4331: 4
- Switch ISR : 3
- Lans 192.168.1.0/24

---
### Security Objectives

The project focuses on **securing administrative access** to networking devices:

- Encrypted **enable secret** password
    
- Enforced **console login password**
    
- **Service password-encryption** applied globally
    
- **SSH remote management** enabled with:
    
    - Domain name: `saeed.local`
        
    - RSA cryptographic keys
        
    - Local user accounts with **secret passwords**
        
- Disabled insecure access methods (Telnet) in favor of **SSH only**
---
## Sample Configuration

### Subnet 1: 192.168.1.0/28
- R1 gig0/0/0 => 192.168.1.1
- S1 => 192.168.1.2
- PCs: 192.168.1.3 <-> 192.168.1.8

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


username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit
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


username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit
```

---

## Need More Details?
This README contains the project overview, subnet plan, and sample configurations.  
If you would like the **full configuration files and additional documentation**, feel free to contact me on **[LinkedIn](https://www.linkedin.com/in/saeed-elfiky-61188b24b/)**.  
