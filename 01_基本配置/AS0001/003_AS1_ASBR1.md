#### 初始化
```text
#
hostname AS1_ASBR1
no ip domain lookup
interface Loopback0
 ip address 10.0.1.3 255.255.255.255
!
interface Ethernet0/0
 ip address 12.0.12.1 255.255.255.0
 no shutdown
!
interface Ethernet0/1
 ip ospf network point-to-point
 ip address 23.0.1.3 255.255.255.0
 no shutdown

line con 0
 exec-timeout 0 0
 logging synchronous
#
#### IGP OSPF
#
router ospf 1
 prefix-suppression
 network 10.0.1.3 0.0.0.0 area 0
 network 23.0.1.3 0.0.0.0 area 0
#
#### LDP
#
mpls ldp router-id Loopback0 force
router ospf 1
 mpls ldp autoconfig
#
```
