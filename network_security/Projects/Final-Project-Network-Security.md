# Network Security Final Project


<p align ="center">
    <img src= "/network_security/photo/NetSec_Final_diagram.png" alt = "cloud deployment"
</p>

## 📌 Overview
This project demonstrates the design and configuration of a secure enterprise network using **Cisco devices**.  
The network implements **subnetting**, **OSPF routing**, and **security best practices** such as **SSH access**, **encrypted and hashed passwords**, and **local authentication**.

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
- `enable secret` configured on every device
- `service password-encryption` enabled
- Console & VTY lines protected with login & password
- Local authentication using: `username saeed secret cisco`

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

### Subnet 2 | 192.168.1.16/28 R2

#### R2 Conf
```
en
conf t
hostname R2
int gig0/0/0 
ip address 192.168.1.17 255.255.255.240
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
network 192.168.1.16 0.0.0.15 area 0

```

#### S2 
```
en
conf t
hostname S2
int vlan 1
ip address 192.168.1.18 255.255.255.240
no shut down
ex
ip default-gateway 192.168.1.17

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

#### S3 Conf

```
en
conf t
hostname S3
int vlan 1
ip address 192.168.1.19 255.255.255.240
no shut down
ex
ip default-gateway 192.168.1.17

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

#### S4 Conf
```
en
conf t
hostname S4
int vlan 1
ip address 192.168.1.20 255.255.255.240
no shut down
ex
ip default-gateway 192.168.1.17

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

#### PCs 
PCs: 
- `192.168.1.21`
- `192.168.1.22`

----
### Subnet 3 | 192.168.1.32/29

#### R3 Conf
```
en
conf t
hostname R3
int gig0/0/0 
ip address 192.168.1.33 255.255.255.248
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
network 192.168.1.32 0.0.0.7 area 0
```

#### S5
```
en
conf t
hostname S5
int vlan 1
ip address 192.168.1.34 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.33

enable secret cisco
line console 0
password cisco
login
exit

service password-encryption
1024

ip domain-name saeed.local
crypto key generate rsa


username saeed secret cisco
line vty 0 4
login local
transport input ssh
exit
```


- PC: `192.168.1.35`
* TACACS+Server: `192.168.1.36`
* RADUIS Server: `192.168.1.37`

----
### Subnet 4 | 192.168.1.40/29 R3

#### R3 Conf
```
en
conf t
int gig0/0/1
ip address 192.168.1.41 255.255.255.248
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
network 192.168.1.40 0.0.0.7 area 0
```

#### S6 Conf

```
en
conf t
hostname S6
int vlan 1
ip address 192.168.1.42 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.41

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

- NTP Server: `192.168.43`
- Syslog Server: `192.168.1.44`


----
### Subnet 5 | 192.168.1.48/29 R4 (DMZ ZONE)

#### R4 Conf

```
en
conf t
hostname R4
int gig0/0/0
ip address 192.168.1.49 255.255.255.248
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
network 192.168.1.48 0.0.0.7 area 0
```

#### S7 Conf

```
en
conf t
hostname S7
int vlan 1
ip address 192.168.1.50 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.49

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

- PC: `192.168.1.51`
- WEB Server: `192.168.1.52`

---
### Subnet 6 | 192.168.1.56/29 R4 (INSIDE ZONE)

#### R4 Conf

```
en
conf t
int gig0/0/1
ip address 192.168.1.57 255.255.255.248
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
network 192.168.1.56 0.0.0.7 area 0
```


#### S8 Conf
```
en
conf t
hostname S8
int vlan 1
ip address 192.168.1.58 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.57

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


- PC: `192.168.1.59` - `192.168.1.60`

---
### Subnet 7 | 192.168.1.64/29 R5

#### R5 Conf
```
en
conf t
hostname R5
int gig0/0/0
ip address 192.168.1.65 255.255.255.248
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
network 192.168.1.64 0.0.0.7 area 0
```


#### S9
```
en
conf t
hostname S9
int vlan 1
ip address 192.168.1.66 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.65

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


- PCs: `192.168.1.67` - `192.168.1.68`

---

### Subnet 8 | 192.168.1.72/29 R6

#### R6 Conf
```
en
conf t
hostname R6
int gig0/0/0
ip address 192.168.1.73 255.255.255.248
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
network 192.168.1.72 0.0.0.7 area 0
```


#### S10
```
en
conf t
hostname S10
int vlan 1
ip address 192.168.1.74 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.73

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


- PC: `192.168.1.75`
- WEB Server 2: `192.168.1.76`

---

### Subnet 9 | 192.168.1.80/29 R7 (TE ST NETWORK & PC)

#### R6 Conf
```
en
conf t
hostname R7
int gig0/0/0
ip address 192.168.1.81 255.255.255.248
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
network 192.168.1.80 0.0.0.7 area 0
```


#### S11
```
en
conf t
hostname S11
int vlan 1
ip address 192.168.1.82 255.255.255.248
no shut down
ex
ip default-gateway 192.168.1.81

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


- PC: `192.168.1.83

---
### Subnet 10 | 192.168.1.88/30 R1 <--> R9

#### R1 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.89 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.88 0.0.0.3 area 0
```

#### R9 Conf
```
en
conf t
hostname R9
int se0/1/0
ip address 192.168.1.90 255.255.255.252
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
network 192.168.1.88 0.0.0.3 area 0
```


----

### Subnet 11 | 192.168.1.92/30 R9 <--> R4

#### R4 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.93 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.92 0.0.0.3 area 0
```

#### R9 Conf
```
en
conf t
int se0/1/1
ip address 192.168.1.94 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.92 0.0.0.3 area 0
```

---
### Subnet 12 | 192.168.1.96/30 R9 <--> R5

#### R9 Conf
```
en
conf t
int se0/2/0
ip address 192.168.1.97 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.96 0.0.0.3 area 0
```

#### R5 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.98 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.96 0.0.0.3 area 0
```

----
### Subnet 13 | 192.168.1.100/30 R9 <--> R8

#### R9 Conf
```
en
conf t
int se0/2/1
ip address 192.168.1.101 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.100 0.0.0.3 area 0
```

#### R8 Conf
```
en
conf t
hostname R8
int se0/2/1
ip address 192.168.1.102 255.255.255.252
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
network 192.168.1.100 0.0.0.3 area 0
```

---
### Subnet 14 | 192.168.1.104/30 R8 <--> R2

#### R2 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.105 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.104 0.0.0.3 area 0
```


#### R8 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.106 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.104 0.0.0.3 area 0
```


---
### Subnet 15 | 192.168.1.108/30 R8 <--> R3

#### R3 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.109 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.108 0.0.0.3 area 0
```


#### R8 Conf
```
en
conf t
int se0/1/1
ip address 192.168.1.110 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.108 0.0.0.3 area 0
```

---
### Subnet 16 | 192.168.1.112/30 R8 <--> R7

#### R8 Conf
```
en
conf t
int se0/2/0
ip address 192.168.1.113 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.112 0.0.0.3 area 0
```


#### R7 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.114 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.112 0.0.0.3 area 0
```

----
### Subnet 17 | 192.168.1.116/30 R6<--> R7

#### R6 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.117 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.117 0.0.0.3 area 0
```


#### R7 Conf
```
en
conf t
int se0/1/0
ip address 192.168.1.118 255.255.255.252
no shut down
ex

router ospf 1
network 192.168.1.116 0.0.0.3 area 0
```

----

  
