### Лабораторная 2
1. Настроить OSPF в Underlay сети для IP связанности между всеми устройствами NXOS

*Глобальная настройка ospf*

`router ospf UNDERLAY` 

`router-id 10.41.0.1` [//см. таблицу адресации](Lab1.md)

`area 0.0.0.0 authentication message-digest` 

`passive-interface default` 
  
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
