### Лабораторная 3
1. Настроить ISIS в Underlay сети для IP связанности между всеми устройствами NXOS

*Глобальная настройка isis*

`router isis UNDERLAY`
`net 49.0001.1111.1111.1111.00`  //уникальный идентификатор под каждое устройство
`is-type level-1`
`authentication-type md5 level-1`
`authentication key-chain gfhjkm_1 level-1`
`address-family ipv4 unicast`

  
*На каждом интерфейсе, участвующем в ospf-маршрутизации:*

`interface EthernetN`

`description to_S2` 

`no switchport` 

`mtu 9192 `

`ip address 10.41.21.6/31 ` [//см. таблицу адресации](Lab1.md)

`ip ospf message-digest-key 1 md5 3 b1b6c42575656fcd `

`ip ospf network point-to-point `

`no ip ospf passive-interface `

`ip router ospf UNDERLAY area 0.0.0.0 `

`no shutdown`
