#### 配置BGP
```text
#
router bgp 2
 no bgp default ipv4-unicast
 neighbor 10.0.2.254 remote-as 2
 neighbor 10.0.2.254 update-source Loopback0
 !
 address-family vpnv4
  neighbor 10.0.2.254 activate
  neighbor 10.0.2.254 send-community extended
#
```

#### 配置VRF信息
```text
#
ip vrf 1
 rd 2:1
 route-target export 2:1
 route-target import 2:1
 
interface Ethernet0/0
 ip vrf forwarding 1
 ip address 12.0.12.2 255.255.255.0
#
```


#### 配置到其他AS的MP-BGP配置
```text
#
router bgp 2
 address-family ipv4 vrf 1
  neighbor 12.0.12.1 remote-as 1
  neighbor 12.0.12.1 activate
  neighbor 12.0.12.1 send-community extended 
#
```