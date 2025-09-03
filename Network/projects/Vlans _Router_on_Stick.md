
# ***Vlans - Trunk - Router-on-Stick***

<p align ="center">
    <img src= "/Network/photo/Vlans_Router_on_Stick.svg" alt = "Vlans - Trunk - Router-on-Stick"
</p>


### Component used
- Router ISR4331
- Switch 2960 IOS15
- 15 PC; 3 for each Department


### **Vlans**
- **VLAN 10 (Sales):** `192.168.10.0/24` > `192.168.10.1`

- **VLAN 20 (HR):** `192.168.20.0/24` >  `192.168.20.1`
    
- **VLAN 30 (DEV):** `192.168.30.0/24` >  `192.168.30.1`
    
- **VLAN 40 (PR):** `192.168.40.0/24` >  `192.168.40.1`
    
- **VLAN 50 (Finance):** `192.168.50.0/24` > `192.168.50.1`

### Ports' Range
- VLAN10: **Fa0/1 - Fa0/3**
- VLAN20: **Fa0/4 - Fa0/6**
- VLAN30: **Fa0/7 - Fa0/9**
- VLAN40: **Fa0/10 - Fa0/12**
- VLAN50: **Fa0/13 - Fa0/15**
- **Trunk Switch Port > Fa 0/16**
- **Trunk Switch Port > GiG 0/0/0**

### Switch Configuration

```
enable
configure terminal


vlan 10
 name Sales
vlan 20
 name HR
vlan 30
 name DEV
vlan 40
 name PR
vlan 50
 name FINANCE
exit


interface range fa0/1 - 3
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
exit

interface range fa0/4 - 6
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
exit

interface range fa0/7 - 9
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
exit

interface range fa0/10 - 12
 switchport mode access
 switchport access vlan 40
 spanning-tree portfast
exit

interface range fa0/13 - 15
 switchport mode access
 switchport access vlan 50
 spanning-tree portfast
exit

interface gi0/1
 switchport mode access
 switchport access vlan 50
 spanning-tree portfast
exit


interface Fa0/16
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
 description TRUNK_TO_ROUTER
exit

end
write memory

show vlan brief
show interfaces trunk

```


### Router-On-Stick

```
enable
configure terminal

interface gig0/0/0
 no shutdown
exit


interface gig0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit

interface gig0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit

interface gig0/0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
exit

interface gig0/0/0.40
 encapsulation dot1Q 40
 ip address 192.168.40.1 255.255.255.0
exit

interface gig0/0/0.50
 encapsulation dot1Q 50
 ip address 192.168.50.1 255.255.255.0
exit

end
write memory

```

