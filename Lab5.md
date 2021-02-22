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
