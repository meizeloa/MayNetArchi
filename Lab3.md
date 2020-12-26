### Лабораторная 3
1. Настроить ISIS в Underlay сети для IP связанности между всеми устройствами NXOS

*Глобальная настройка isis*

`router isis UNDERLAY`

`net 49.0001.1111.1111.1111.00`  //уникальный идентификатор под каждое устройство

`is-type level-1`

`authentication-type md5 level-1`

`authentication key-chain ISIS_AUTH level-1`

`address-family ipv4 unicast`

*Настройка авторизации*

`key chain ISIS_AUTH`

`key 1`

`key-string 7 070827444402143a46`

*На каждом интерфейсе, устанавливающем isis-соседство:*

`interface EthernetN`

`description to_S2` 

`no switchport` 

`ip address 10.41.21.6/31 ` [//см. таблицу адресации](Lab1.md)

`ip router isis UNDERLAY`

`isis network point-to-point `

`no shutdown`

*На интерфейсе, объявляющем свою сеть, но не устанавливающем соседство:*

`interface EthernetN`

`description to_R2` 

`no switchport` 

`ip address 10.41.31.1/30 ` [//см. таблицу адресации](Lab1.md)

`ip router isis UNDERLAY`

`isis passive-interface level-1`

`no shutdown`
