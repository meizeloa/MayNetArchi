### Лабораторная 5
1. Настроить PIM в сети

#### Топология сети
![](underlay-net-bgp.PNG)

<details>
  <summary>RX</summary>
<pre><code>
ip multicast-routing
int ran e0/0-2
 ip pim sparse-mode
</code></pre>
</details>
<details>
  <summary>Spine</summary>
<pre><code>
feature pim
int e1/X
ip pim sparse-mode
</code></pre>
</details>
<details>
  <summary>Leaves</summary>
<pre><code>
feature pim
int e1/X
ip pim sparse-mode
</code></pre>
</details>
