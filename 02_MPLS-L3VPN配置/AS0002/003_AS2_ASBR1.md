#### 配置BGP

```text
router bgp 2
 no bgp default route-target filter
 no bgp default ipv4-unicast
 neighbor 10.0.2.254 remote-as 2
 neighbor 10.0.2.254 update-source Loopback0
 !
 address-family vpnv4
  neighbor 10.0.2.254 activate
  neighbor 10.0.2.254 send-community extended
  neighbor 10.0.2.254 next-hop-self

```

#### 配置到其他AS的MP-BGP配置

```text
router bgp 2
 neighbor 12.0.12.1 remote-as 1
 address-family vpnv4
  neighbor 12.0.12.1 activate
  neighbor 12.0.12.1 send-community extended 

interface Ethernet0/0
 mpls bgp forwarding
 
```