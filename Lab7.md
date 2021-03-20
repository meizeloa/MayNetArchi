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

sh vpc

Legend:
                (*) - local vPC is down, forwarding via vPC peer-link

vPC domain id                     : 1
Peer status                       : peer adjacency formed ok
vPC keep-alive status             : peer is alive
Configuration consistency status  : success
Per-vlan consistency status       : success
Type-2 consistency status         : success
vPC role                          : secondary
Number of vPCs configured         : 0
Peer Gateway                      : Disabled
Dual-active excluded VLANs        : -
Graceful Consistency Check        : Enabled
Auto-recovery status              : Disabled
Delay-restore status              : Timer is off.(timeout = 30s)
Delay-restore SVI status          : Timer is off.(timeout = 10s)
Operational Layer3 Peer-router    : Disabled

vPC Peer-link status
---------------------------------------------------------------------
id    Port   Status Active vlans
--    ----   ------ -------------------------------------------------
1     Po99   up     1,10
