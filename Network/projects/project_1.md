Router's password: saeed

### Router Setting
interface gig0/0/0

10.0.0.0/28
10.0.0.1 => Router
10.0.0.2 => Switch

```
enable
conf t
interface gig0/0/0
ip address 10.0.0.1 255.255.255.240
exit
end
write memory


conf t
interface gig0/0/1
ip address 10.0.0.17 255.255.255.248
exit
end
write memory
```

### Switch 1
```
enable
conf t
interface vlan 1
ip address 10.0.0.2 255.255.255.240
exit
ip default-gateway 10.0.0.1
exit
write memory
```


### PCs In Switch 1

```
PC 1
open desktop
IP configuration
ip = 10.0.0.3
subnet = 255.255.255.240
gateway = 10.0.0.1


PC 2
open desktop
IP configuration
ip = 10.0.0.4
subnet = 255.255.255.240
gateway = 10.0.0.1



PC 3
open desktop
IP configuration
ip = 10.0.0.5
subnet = 255.255.255.240
gateway = 10.0.0.1
```

### Switch 2

```
enable
conf t
interface vlan 1
ip address 10.0.0.18 255.255.255.248
exit
ip default-gateway 10.0.0.17
exit
write memory
```


### PCs in Switch 2
```
PC 1
open desktop
IP configuration
ip = 10.0.0.19
subnet = 255.255.255.248
gateway = 10.0.0.17
```
