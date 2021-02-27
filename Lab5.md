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

Подпишем интерфейс R2 e0/0 на группу рассылки:

_ip igmp static-group 224.1.1.1_

В таблице mroute появится маршрут с неизвестным адресом источника и адресом назначения:

_(*, 224.1.1.1), 4d17h/stopped, RP 10.41.2.1, flags: SJPC_

_Incoming interface: Ethernet0/0, RPF nbr 10.41.32.1_
  
_Outgoing interface list: Null_

R1 знает об интерфейсе назначения мультикаста:

_(*, 224.1.1.1), 3d13h/00:02:51, RP 10.41.2.1, flags: S
  Incoming interface: Null, RPF nbr 0.0.0.0
  Outgoing interface list:
    Ethernet0/1, Forward/Sparse, 3d13h/00:02:51

S2 знает об интерфейсе RandevouzPoint и интерфейсе назначения:

(*, 224.1.1.1/32), uptime: 3d14h, pim ip

  Incoming interface: Ethernet1/1, RPF nbr: 10.41.12.1
  
  Outgoing interface list: (count: 1) Ethernet1/3, uptime: 3d14h, pim
  
L2 знает об интерфейсе RandevouzPoint и интерфейсе назначения:

(*, 224.1.1.1/32), uptime: 3d14h, pim ip
  
  Incoming interface: Ethernet1/3, RPF nbr: 10.41.22.7
  
  Outgoing interface list: (count: 1) Ethernet1/1, uptime: 3d14h, pim
