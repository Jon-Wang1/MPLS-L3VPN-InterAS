### 配置BGP
```text
#
router bgp 1
 no bgp default ipv4-unicast
 neighbor 10.0.1.254 remote-as 1
 neighbor 10.0.1.254 update-source Loopback0
 !
 address-family vpnv4
  neighbor 10.0.1.254 activate
  neighbor 10.0.1.254 send-community extended
#
```

#### 配置VRF信息
```text
#
ip vrf 1
 rd 1:1
 route-target export 1:1
 route-target import 1:1
 
interface Ethernet0/0
 ip vrf forwarding 1
 ip address 12.0.12.1 255.255.255.0
#
```

#### 配置到其他AS的MP-BGP配置
```text
#
router bgp 1
 address-family ipv4 vrf 1
  neighbor 12.0.12.2 remote-as 2
  neighbor 12.0.12.2 activate
  neighbor 12.0.12.2 send-community extended 
#
```