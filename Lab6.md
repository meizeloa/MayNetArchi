### Лабораторная 6
1. Настроить Overlay на основе VxLAN EVPN для L2 связанности между клиентами

#### Топология сети
![](underlay-net-bgp.PNG)

<details>
  <summary>SPINE</summary>
<pre><code>
feature nv overlay
nv overlay evpn

router bgp 65001
  address-family ipv4 unicast
    network 10.41.1.1/32
    network 10.41.11.0/30
    network 10.41.21.4/31
    network 10.41.22.4/31
    network 10.41.23.4/31
  template peer LEAF
    update-source loopback0
    address-family l2vpn evpn
      send-community
      send-community extended
      route-reflector-client
  neighbor 10.41.11.1
    remote-as 65000
    address-family ipv4 unicast
  neighbor 10.41.21.4
    inherit peer LEAF
    remote-as 65010
    address-family ipv4 unicast
  neighbor 10.41.22.4
    inherit peer LEAF
    remote-as 65020
    address-family ipv4 unicast
  neighbor 10.41.23.4
    inherit peer LEAF
    remote-as 65030
    address-family ipv4 unicast
</code></pre></details>
