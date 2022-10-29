#### 配置BGP

no bgp default route-target filter 该命令的作用是即使本地没有对应的rt，也保留接收到的路由。

```text
router bgp 1
 no bgp default route-target filter
 no bgp default ipv4-unicast
 neighbor 10.0.1.254 remote-as 1
 neighbor 10.0.1.254 update-source Loopback0
 !
 address-family vpnv4
  neighbor 10.0.1.254 activate
  neighbor 10.0.1.254 send-community extended
  neighbor 10.0.1.254 next-hop-self
  
```

#### 配置到其他AS的MP-BGP配置

```text
router bgp 1
 neighbor 12.0.12.2 remote-as 2
 address-family vpnv4
  neighbor 12.0.12.2 activate
  neighbor 12.0.12.2 send-community extended 

interface Ethernet0/0
 mpls bgp forwarding
 
```
