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
### Subnet 2 AND 3: 
1. 192.168.1.16/29 
	- R4 gig0/0/0=> 192.168.1.17/29
	- S2 => 192.168.1.18
	- PCs: 192.168.1.19 <-> 192.168.1.20

2. 192.168.1.24/29 
	- R4 gig0/0/1=> 192.168.1.25/29
	- S3 => 192.168.1.26
	- PC: 192.168.1.27
#### R4 Conf
```
en
conf t
hostname R4
int gig0/0/0 
ip address 192.168.1.17 255.255.255.248
no shut down
ex

int gig0/0/1 
ip address 192.168.1.25 255.255.255.248
no shut down
ex

enable secret cisco
line console 0
password cisco
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

#### S2 Conf
```
en
conf t
hostname S2
int vlan 1
ip address 192.168.1.18 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.17

enable secret cisco
line console 0
password cisco
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


#### S3 Conf
```
en
conf t
hostname S3
int vlan 1
ip address 192.168.1.26 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.25

enable secret cisco
line console 0
password cisco
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


----
### Subnet 4: 192.168.1.32/30 R1 -R2
- R1 Se0/1/0 =>192.168.1.33/ 30
- R2 Se0/1/0 =>192.168.1.34/ 30


#### R1 Conf
```
en
conf t
int se0/1/0 
ip address 192.168.1.33 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.0 0.0.0.15 area 0
network 192.168.1.32 0.0.0.3 area 0
ex

```

#### R2 conf
```
en
conf t
hostname R2
int se0/1/0 
ip address 192.168.1.34 255.255.255.252
no shut down
ex

enable secret cisco
line console 0
password cisco
exit

service password-encryption


ip domain-name saeed.local
crypto key generate rsa


username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit


router ospf 1
network 192.168.1.32 0.0.0.3 area 0
ex
```


---
### Subnet 5: 192.168.1.36/30 R2 -R3
- R2 Se0/1/1 =>192.168.1.37/ 30
- R3 Se0/1/0 =>192.168.1.38/ 30

#### R2
```
en
conf t
int se0/1/1 
ip address 192.168.1.37 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.36 0.0.0.3 area 0
ex

```

#### R3 
```
en
conf t
hostname R3
int se0/1/0 
ip address 192.168.1.38 255.255.255.252
no shut down
ex

enable secret cisco
line console 0
password cisco
exit

service password-encryption


ip domain-name saeed.local
crypto key generate rsa


username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit


router ospf 1
network 192.168.1.36 0.0.0.3 area 0
ex

```

---
### Subnet 6: 192.168.1.40/30 R3 -R4
- R3 Se0/1/1 =>192.168.1.41/ 30
- R3 Se0/1/0 =>192.168.1.42/ 30

#### R3 Conf

```
en
conf t
int se0/1/1 
ip address 192.168.1.41 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.40 0.0.0.3 area 0
ex

```

#### R4 Conf
```
en
conf t
int se0/1/0 
ip address 192.168.1.42 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.40 0.0.0.3 area 0
network 192.168.1.16 0.0.0.7 area 0
network 192.168.1.24 0.0.0.7 area 0
ex
```

