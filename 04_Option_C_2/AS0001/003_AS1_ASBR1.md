#### 配置BGP IPv4，并使能分发标签能力

```text
router bgp 1
 no bgp default ipv4-unicast
 neighbor 10.0.1.254 remote-as 1
 neighbor 10.0.1.254 update-source Loopback0
 neighbor 12.0.12.2 remote-as 2
 !
 address-family ipv4
  neighbor 10.0.1.254 activate
  neighbor 10.0.1.254 next-hop-self
  neighbor 10.0.1.254 send-label
  neighbor 12.0.12.2 activate
  neighbor 12.0.12.2 send-label

```

#### 在面向其他AS的接口上启动mpls转发、接受能力

```text
interface Ethernet0/0
 mpls bgp forwarding

```
