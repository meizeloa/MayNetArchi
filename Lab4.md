### Лабораторная 4
1. Настроить BGP в Underlay сети для IP связанности между всеми устройствами сети

#### Топология сети
![](underlay-bgp.PNG)

<details>
  <summary>R1</summary>
<pre><code>
router bgp 65000
 bgp log-neighbor-changes
 neighbor 10.41.11.2 remote-as 65001   //to S1
 neighbor 10.41.12.2 remote-as 65001   //to S2
 neighbor 10.41.13.2 remote-as 65002   //to S3
 !
 address-family ipv4
  network 10.41.11.0 mask 255.255.255.252
  network 10.41.12.0 mask 255.255.255.252
  network 10.41.13.0 mask 255.255.255.252
  neighbor 10.41.11.2 activate
  neighbor 10.41.12.2 activate
  neighbor 10.41.13.2 activate
  maximum-paths 3
</code></pre>
</details>
<details>
  <summary>Spine</summary>
<pre><code>
feature bgp
router bgp 65001
  address-family ipv4 unicast
    network 10.41.11.0/30
    network 10.41.21.4/31
    network 10.41.22.4/31
    network 10.41.23.4/31
  neighbor 10.41.11.1               //to R1
    remote-as 65000
    address-family ipv4 unicast
  neighbor 10.41.21.4               //to L1
    remote-as 65010
    address-family ipv4 unicast
  neighbor 10.41.22.4               //to L2
    remote-as 65020
    address-family ipv4 unicast
  neighbor 10.41.23.4               //to L3
    remote-as 65030
    address-family ipv4 unicast
</code></pre>
</details>
