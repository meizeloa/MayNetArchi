### Лабораторная 6
1. Настроить VPC 

#### Топология сети
![](vpc.PNG)

<details>
  <summary>LEAF</summary>
<pre><code>
feature vpc
feature lacp

vrf context KEEP

vpc domain 1
  peer-keepalive destination 10.41.3.2 source 10.41.3.1 vrf KEEP

interface port-channel99
  switchport mode trunk
  spanning-tree port type network
  vpc peer-link

interface port-channel1
  switchport mode trunk

interface Ethernet1/1
  description to_R2
  switchport mode trunk
  channel-group 1 mode active

interface Ethernet1/4
  description to_L2
  no switchport
  vrf member KEEP
  ip address 10.41.3.1/30
  no shutdown

interface Ethernet1/5
  switchport mode trunk
  channel-group 99 mode active

interface Ethernet1/6
  switchport mode trunk
  channel-group 99 mode active
  
</code></pre></details>
