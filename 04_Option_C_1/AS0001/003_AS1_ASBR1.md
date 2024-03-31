#### 配置BGP,将RR和PE的环回口路由通告至AS2

```text
router bgp 1
 no bgp default ipv4-unicast
 neighbor 12.0.12.2 remote-as 2
 !
 address-family ipv4
  network 10.0.1.1 mask 255.255.255.255
  network 10.0.1.254 mask 255.255.255.255
  neighbor 12.0.12.2 activate

```

#### 配置OSPF,将外部的RR和PE的环回口路由重分布至AS1

```text
ip prefix-list FOREIGN_Lo0 seq 5 permit 10.0.2.1/32
ip prefix-list FOREIGN_Lo0 seq 10 permit 10.0.2.254/32

route-map FOREIGN_Lo0 permit 10
 match ip address prefix-list FOREIGN_Lo0
 
router ospf 1
 redistribute bgp 1 subnets route-map FOREIGN_Lo0

```

#### 配置BGP，对其他AS的EBGP邻居启用发送标签能力

```text
router bgp 1
 address-family ipv4
  neighbor 12.0.12.2 send-label

```

#### 在面向其他AS的接口上启动mpls转发、接受能力

```text
interface Ethernet0/0
 mpls bgp forwarding

```
