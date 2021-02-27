### Лабораторная 5
1. Настроить PIM в сети

#### Топология сети
![](underlay-net-bgp.PNG)

<details>
  <summary>RX</summary>
<pre><code>
ip multicast-routing
ip pim rp-address 10.41.2.1
int ran e0/0-2
 ip pim sparse-mode
int Lo0
 ip pim sparse-mode
</code></pre>
</details>
<details>
  <summary>Spine</summary>
<pre><code>
feature pim
ip pim rp-address 10.41.2.1
int e1/X
ip pim sparse-mode
</code></pre>
</details>
<details>
  <summary>Leaves</summary>
<pre><code>
feature pim
ip pim rp-address 10.41.2.1
int e1/X
ip pim sparse-mode
</code></pre>
</details>

<h6>Подпишем интерфейс R2 e0/0 на группу рассылки:</h6>

_ip igmp static-group 224.1.1.1_

В таблице mroute появится маршрут с неизвестным адресом источника и адресом назначения:

_(*, 224.1.1.1), 4d17h/stopped, RP 10.41.2.1, flags: SJPC_

_Incoming interface: Ethernet0/0, RPF nbr 10.41.32.1_
  
_Outgoing interface list: Null_

R1 знает об интерфейсе назначения мультикаста:

_(*, 224.1.1.1), 3d13h/00:02:51, RP 10.41.2.1, flags: S_

_Incoming interface: Null, RPF nbr 0.0.0.0_

_Outgoing interface list: Ethernet0/1, Forward/Sparse, 3d13h/00:02:51_

S2 знает об интерфейсе RandevouzPoint и интерфейсе назначения:

_(*, 224.1.1.1/32), uptime: 3d14h, pim ip_

_Incoming interface: Ethernet1/1, RPF nbr: 10.41.12.1_
  
_Outgoing interface list: (count: 1) Ethernet1/3, uptime: 3d14h, pim_
  
L2 знает об интерфейсе RandevouzPoint и интерфейсе назначения:

_(*, 224.1.1.1/32), uptime: 3d14h, pim ip_
  
_Incoming interface: Ethernet1/3, RPF nbr: 10.41.22.7_
  
_Outgoing interface list: (count: 1) Ethernet1/1, uptime: 3d14h, pim_


<h5>Запустим ping 224.1.1.1 на R3 в качестве источника мультикаста:</h5>

Маршрут построился: R3->L1->S2->L3->R2

_(*, 224.1.1.1), 00:00:24/stopped, RP 10.41.2.1, flags: SPF_

_Incoming interface: Ethernet0/0, RPF nbr 10.41.31.1_

_Outgoing interface list: Null_


_(10.41.2.3, 224.1.1.1), 00:00:24/00:02:35, flags: PFT_

_Incoming interface: Loopback0, RPF nbr 0.0.0.0, Registering_

_Outgoing interface list: Null_


_(10.41.31.2, 224.1.1.1), 00:00:24/00:02:35, flags: PFT_

_Incoming interface: Ethernet0/0, RPF nbr 0.0.0.0, Registering_

_Outgoing interface list: Null_

L1

_(10.41.31.2/32, 224.1.1.1/32), uptime: 00:01:56, ip pim_

_Incoming interface: Ethernet1/1, RPF nbr: 10.41.31.2_

_Outgoing interface list: (count: 1) Ethernet1/3, uptime: 00:01:55, pim_

S2

_(*, 224.1.1.1/32), uptime: 3d15h, pim ip_

_Incoming interface: Ethernet1/1, RPF nbr: 10.41.12.1_

_Outgoing interface list: (count: 1)  Ethernet1/3, uptime: 3d15h, pim_


_(10.41.31.2/32, 224.1.1.1/32), uptime: 00:08:08, pim mrib ip_

_Incoming interface: Ethernet1/2, RPF nbr: 10.41.21.6_

_Outgoing interface list: (count: 1) Ethernet1/4, uptime: 00:08:07, pim_

L2 

_(*, 224.1.1.1/32), uptime: 3d15h, pim ip_

_Incoming interface: Ethernet1/3, RPF nbr: 10.41.22.7_

_Outgoing interface list: (count: 1)  Ethernet1/1, uptime: 3d15h, pim_
    
L3

_(10.41.31.2/32, 224.1.1.1/32), uptime: 00:03:54, pim ip_

_Incoming interface: Ethernet1/3, RPF nbr: 10.41.23.7_

_Outgoing interface list: (count: 1)   Ethernet1/1, uptime: 00:03:54, pim_


R2

_(10.41.31.2, 224.1.1.1), 00:00:41/00:02:18, flags: JT_

_Incoming interface: Ethernet0/1, RPF nbr 10.41.33.1_

_Outgoing interface list:  Ethernet0/0, Forward/Sparse, 00:00:41/00:02:18, A_
