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
ip igmp static-group 224.1.1.1

В таблице mroute появится маршрут:
(*, 224.1.1.1), 4d17h/stopped, RP 10.41.2.1, flags: SJPC
  Incoming interface: Ethernet0/0, RPF nbr 10.41.32.1
  Outgoing interface list: Null
