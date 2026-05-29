## Домашнее задание №1
#### Проектирование сети

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/Pro/Lab1/img/1.jpg?raw=true)

Цель:
распланировать адресное пространство, настроить IP на активных портах для дальнейшей работы над проектом и задокументировать адресацию.

------------

#### Разработаете и задокументируете адресное пространство для лабораторного стенда.

#### 1. Сеть управления (MGMT) и Loopback интерфейсы
|  Устройство |  IP-Адрес | MGMT VLAN | Loopback |Коментарий |
| ------------ | ------------ |------------ | ------------ | ------------ |
|  SW2 | 10.255.254.2/24 |999|10.255.255.2/32||
|  SW3 | 10.255.254.3/24 |999|10.255.255.3/32||
|  SW4 | 10.255.254.4/24 |999|10.255.255.4/32||
|  SW5 | 10.255.254.5/24 |999|-||
|  SW9 | 10.255.254.9/24 |999|-||
|  SW10 | 10.255.254.10/24 |999|-||
|  R12 | 10.255.254.12/24 |999|10.255.255.12/32||
|  R13 | 10.255.254.13/24 |999|10.255.255.13/32||
|  R14 | 10.255.254.14/24 |999|10.255.255.14/32||
|  R15 | 10.255.254.15/24 |999|10.255.255.15/32||
|  R16 | 10.255.254.16/24 |999|10.255.255.16/32||
|  R17 | 10.255.254.17/24 |999|10.255.255.17/32||
|  R18 | 10.255.254.18/24 |999|10.255.255.18/32||
|  R19 | 10.255.254.19/24 |999|10.255.255.19/32||
|  R20 | 10.255.254.20/24 |999|10.255.255.20/32||
|  R21 | 10.255.254.21/24 |999|10.255.255.21/32||
|  R22 | 10.255.254.22/24 |999|10.255.255.22/32||
|  R23 | 10.255.254.23/24 |999|10.255.255.23/32||
|  R24 |10.255.254.24/24 |999|10.255.255.24/32||
|  R25 | 10.255.254.25/24 |999|10.255.255.25/32||
|  R26 | 10.255.254.26/24 |999|10.255.255.26/32||
|  R27 | 10.255.254.27/24 |999|10.255.255.27/32||
|  R28 | 10.255.254.28/24 |999|10.255.255.28/32||
|  SW29 | 10.255.254.29/24 |999|-||
|  R32 |  10.255.254.32/24 |999|10.255.255.32/32|||

------------

#### 2. Loopback интерфейсы
|  Устройство |  IP-Адрес | Коментарий |
| ------------ | ------------ |------------ |
|  R12 |  10.255.255.12/32||
|  R13 |  10.255.255.13/32||
|  R14 |  10.255.255.14/32||
|  R15 |  10.255.255.15/32||
|  R16 |  10.255.255.16/32||
|  R17 |  10.255.255.17/32||
|  R18 |  10.255.255.18/32||
|  R19 |  10.255.255.19/32||
|  R20 |  10.255.255.20/32||
|  R21 |  10.255.255.21/32||
|  R22 |  10.255.255.22/32||
|  R23 |  10.255.255.23/32||
|  R24 |  10.255.255.24/32||
|  R25 |  10.255.255.25/32||
|  R26 |  10.255.255.26/32||
|  R27 |  10.255.255.27/32||
|  R28 |  10.255.255.28/32||
|  R32 |  10.255.255.32/32|||

------------

#### 3. Клиентские LAN-сегменты
|  Устройство |  IP-Адрес | Шлюз | Vlan | Коментарий |
| ------------ | ------------ |------------ |------------ | ------------ |
|  VPC1 |192.168.10.11/24| 192.168.10.1 |10| | 
|  VPC7 | 192.168.11.11/24|192.168.11.1| 11| | 
|  VPC6 | 192.168.20.11/24|192.168.20.1| 20| | 
|  VPC8 | 192.168.21.11/24| 192.168.21.1|21| | 
|  VPC30 | 192.168.30.11/24| 192.168.30.1|30| | 
|  VPC31 | 192.168.31.11/24| 192.168.31.1|31| | | 

------------

#### 4. Vlan на портах коммутаторов
|  Устройство | Порт | IP-Адрес | Шлюз | Vlan | Коментарий |
| ------------ | ------------ |------------ |------------ | ------------ | ------------ |
|  SW2 | e0/0 |-|-| trunk 11, 999 ||
|  SW2 | e0/1 |-|-| trunk 11, 999||
|  SW2 | e0/2 |-|-| access 11||
|  SW3 | e0/0 |-|-| trunk 10, 999 ||
|  SW3 | e0/1 |-|-| trunk 10, 999||
|  SW3 | e0/2 |-|-| access 10||
|  SW4 | e0/0 |-|-| trunk 10, 999 ||
|  SW4 | e0/1 |-|-| trunk 11, 999||
|  SW4 | e0/2 |-|-| trunk 10, 11,999 ||
|  SW4 | e0/3 |-|-| trunk 10, 11,999 ||
|  SW4 | e1/0 |-|-|  trunk 10, 11,999||
|  SW5 | e0/0 |-|-| trunk 11, 999 ||
|  SW5 | e0/1 |-|-| trunk 10, 999||
|  SW5 | e0/2 |-|-| trunk 10, 11,999 ||
|  SW5 | e0/3 |-|-| trunk 10, 11,999 ||
|  SW5 | e1/0 |-|-|  trunk 10, 11,999||
|  SW9 | e0/0 |-|-| trunk 21, 999 ||
|  SW9 | e0/1 |-|-| trunk 21, 999||
|  SW9 | e0/2 |-|-| access 21||
|  SW10 | e0/0 |-|-| trunk 20, 999 ||
|  SW10 | e0/1 |-|-| trunk 20, 999||
|  SW10 | e0/2 |-|-| access 20||
|  SW29 | e0/0 |-|-| access 30,31 ||
|  SW29 | e0/1 |-|-| trunk 30,31, 999||
|  SW29 | e0/2 |-|-| trunk 30,31, 999|||

------------


#### 5. IP-Адреса на маршрутизаторах
|  Устройство1 | Порт | IP-Адрес |  Устройство2 | Порт | IP-Адрес | Шлюз | Vlan | Коментарий |
| ------------ | ------------ |------------ |------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  R12 | e0/0 |-| SW4 | e1/0 |-||| Москва |
|  R12 | e0/1 |-| SW5 | e1/1 |-||| Москва |
|  R12 | e0/2 | 10.255.253.1/30 | R14 | e0/0 |10.255.253.2/30||| Москва |
|  R12 | e0/3 | 10.255.253.5/30 | R15 | e0/1 |10.255.253.6/30||| Москва |
|  R13 | e0/0 |-| SW5 | e1/0 |-||| Москва |
|  R13 | e0/1 |-| SW4 | e1/1 |-||| Москва |
|  R13 | e0/2 | 10.255.253.9/30 | R15 | e0/0 | 10.255.253.10/30 ||| Москва |
|  R13 | e0/3 | 10.255.253.13/30 | R14 | e0/1 | 10.255.253.14/30 ||| Москва |
|  R14 | e0/0 | 10.255.253.2/30 | R12 | e0/2 | 10.255.253.1/30 ||| Москва |
|  R14 | e0/1 |10.255.253.10/30 | R13 | e0/3 | 10.255.253.9/30 ||| Москва |
|  R14 | e0/2 | 10.255.253.17/30 | R22 | e0/0 |10.255.253.18/30||| Москва |
|  R14 | e0/3 | 10.255.253.21/30 | R19 | e0/0 |10.255.253.22/30||| Москва |
|  R15 | e0/0 | 10.255.253.10/30 | R13 | e0/2 | 10.255.253.9/30 ||| Москва |
|  R15 | e0/1 |10.255.253.6/30 | R12 | e0/3 | 10.255.253.5/30 ||| Москва |
|  R15 | e0/2 | 10.255.253.25/30 | R21 | e0/0 |10.255.253.26/30||| Москва |
|  R15 | e0/3 | 10.255.253.29/30 | R20 | e0/0 |10.255.253.30/30||| Москва |
|  R16 | e0/0 | - | SW10 | e0/3 | - ||| СПетербург |
|  R16 | e0/1 |10.255.253.33/30 | R18 | e0/0 | 10.255.253.34/30 ||| СПетербург |
|  R16 | e0/2 | - | SW9 | e1/0 | - ||| СПетербург |
|  R16 | e0/3 | 10.255.253.37/30 | R32 | e0/0 |10.255.253.38/30||| СПетербург |
|  R17 | e0/0 | - | SW9 | e0/3 | - ||| СПетербург |
|  R17 | e0/1 |10.255.253.41/30 | R18 | e0/1 | 10.255.253.42/30 ||| СПетербург |
|  R17 | e0/2 | - | SW10 | e1/0 | - ||| СПетербург |
|  R18 | e0/0 | 10.255.253.34/30 | R16 | e0/1 | 10.255.253.33/30 ||| СПетербург |
|  R18 | e0/1 |10.255.253.42/30 | R17 | e0/1 | 10.255.253.41/30 ||| СПетербург |
|  R18 | e0/2 | 10.255.253.45/30 | R24 | e0/3 |10.255.253.46/30||| СПетербург |
|  R18 | e0/3 | 10.255.253.49/30 | R26 | e0/3 |10.255.253.50/30||| СПетербург |
|  R19 | e0/0 | 10.255.253.22/30 | R14 | e0/3 |10.255.253.21/30||| Москва |
|  R20 | e0/0 | 10.255.253.30/30 | R15 | e0/3 |10.255.253.29/30||| Москва |
|  R21 | e0/0 | 10.255.253.26/30 | R15 | e0/2 |10.255.253.25/30||| Ламас |
|  R21 | e0/1 | 10.255.253.53/30 | R22 | e0/1 |10.255.253.54/30||| Ламас |
|  R21 | e0/2 | 10.255.253.57/30 | R24 | e0/0 |10.255.253.58/30||| Ламас |
|  R22 | e0/0 | 10.255.253.18/30 | R14 | e0/2 |10.255.253.17/30||| Киторн |
|  R22 | e0/1 | 10.255.253.54/30 | R21 | e0/1 |10.255.253.53/30||| Киторн |
|  R22 | e0/2 | 10.255.253.61/30 | R23 | e0/0 |10.255.253.62/30||| Киторн |
|  R23 | e0/0 | 10.255.253.62/30 | R22 | e0/2 |10.255.253.61/30||| Триада |
|  R23 | e0/1 | 10.255.253.65/30 | R25 | e0/0 |10.255.253.66/30||| Триада |
|  R23 | e0/2 | 10.255.253.69/30 | R24 | e0/2 |10.255.253.70/30||| Триада |
|  R24 | e0/0 | 10.255.253.58/30 | R21 | e0/2 |10.255.253.57/30||| Триада |
|  R24 | e0/1 | 10.255.253.73/30 | R26 | e0/0 |10.255.253.74/30||| Триада |
|  R24 | e0/2 | 10.255.253.70/30 | R23 | e0/2 |10.255.253.69/30||| Триада |
|  R25 | e0/0 | 10.255.253.66/30 | R23 | e0/1 |10.255.253.65/30||| Триада |
|  R25 | e0/1 | 10.255.253.77/30 | R27 | e0/0 |10.255.253.78/30||| Триада |
|  R25 | e0/2 | 10.255.253.81/30 | R26 | e0/2 |10.255.253.82/30||| Триада |
|  R25 | e0/3 | 10.255.253.85/30 | R28 | e0/1 |10.255.253.86/30||| Триада |
|  R26 | e0/0 | 10.255.253.74/30 | R24 | e0/1 |10.255.253.73/30||| Триада |
|  R26 | e0/1 | 10.255.253.89/30 | R28 | e0/0 |10.255.253.90/30||| Триада |
|  R26 | e0/2 | 10.255.253.82/30 | R25 | e0/2 |10.255.253.81/30||| Триада |
|  R26 | e0/3 | 10.255.253.50/30 | R18 | e0/3 |10.255.253.49/30||| Триада |
|  R27 | e0/0 | 10.255.253.78/30 | R25 | e0/1 |10.255.253.77/30||| Лабытнанги |
|  R28 | e0/0 | 10.255.253.90/30 | R26 | e0/1 |10.255.253.89/30||| Чукурдах |
|  R28 | e0/1 | 10.255.253.86/30 | R25 | e0/3 |10.255.253.85/30||| Чукурдах |
|  R28 | e0/2 | - | SW29 | e0/2 | - ||| Чукурдах |
|  R32 | e0/0 | 10.255.253.38/30 | R16 | e0/3 |10.255.253.37/30||| СПетербург |











#### Настройка SW3
<details>
	
	123
	1231
    123
	 
</details>

------------

#### Настройка SW2
<details>
    SW2#show running-config
    Building configuration...

    Current configuration : 1774 bytes
    !
    ! Last configuration change at 07:20:52 UTC Thu May 28 2026
    !
    version 15.1
    service timestamps debug datetime msec
    service timestamps log datetime msec
    service password-encryption
    service compress-config
    !
    hostname SW2
    !
    boot-start-marker
    boot-end-marker
    !
    !
    enable secret 4 X4ZqtPJ///KxuEWxHSsJrv3beQVnz2ise/xj8fF6eFU
    !
    username admin privilege 15 secret 4 X4ZqtPJ///KxuEWxHSsJrv3beQVnz2ise/xj8fF6eFU
    no aaa new-model
    !
    ip cef
    !
    !
    no ip domain-lookup
    ip domain-name otus.ru
    no ipv6 cef
    ipv6 multicast rpf use-bgp
    !
    !
    !
    !
    !
    !
    !
    !
    spanning-tree mode rapid-pvst
    spanning-tree extend system-id
    spanning-tree vlan 1-4094 priority 61440
    !
    !
    !
    !
    vlan internal allocation policy ascending
    !
    ip ssh version 2
    !
    !
    !
    !
    !
    !
    !
    !
    !
    interface Loopback0
     ip address 10.255.255.2 255.255.255.255
    !
    interface Ethernet0/0
     description TO-SW5-E0/0
     switchport trunk encapsulation dot1q
     switchport trunk allowed vlan 70,999
     switchport mode trunk
     duplex auto
    !
    interface Ethernet0/1
     description TO-SW4-E0/1
     switchport trunk encapsulation dot1q
     switchport trunk allowed vlan 70,999
     switchport mode trunk
     duplex auto
    !
    interface Ethernet0/2
     description TO-VPC7
     switchport access vlan 70
     switchport mode access
     duplex auto
     spanning-tree portfast
    !
    interface Ethernet0/3
     duplex auto
    !
    interface Ethernet1/0
     duplex auto
    !
    interface Ethernet1/1
     duplex auto
    !
    interface Ethernet1/2
     duplex auto
    !
    interface Ethernet1/3
    duplex auto
    !
    interface Vlan999
     description MANAGEMENT
     ip address 10.255.254.2 255.255.255.0
    !
    ip default-gateway 10.255.254.254
    !
    no ip http server
    !
    !
    !
    !
    !
    control-plane
    !
    banner motd ^CSW2^C
    !
    line con 0
     exec-timeout 5 0
     logging synchronous
     login local
    line aux 0
    line vty 0 4
     exec-timeout 5 0
     logging synchronous
     login local
     transport input ssh
    !
    end
	
	SW2#show vlan brief
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3
    70   VPC7                             active    Et0/2
    999  MANAGEMENT                       active
    1002 fddi-default                     act/unsup
    1003 token-ring-default               act/unsup
    1004 fddinet-default                  act/unsup
    1005 trnet-default                    act/unsup

</details>

#### Настройка SW3
<details>

    SW3#show running-config
    Building configuration...
    
    Current configuration : 1784 bytes
    !
    ! Last configuration change at 06:37:09 UTC Thu May 28 2026
    !
    version 15.1
    service timestamps debug datetime msec
    service timestamps log datetime msec
    service password-encryption
    service compress-config
    !
    hostname SW3
    !
    boot-start-marker
    boot-end-marker
    !
    !
    enable secret 4 X4ZqtPJ///KxuEWxHSsJrv3beQVnz2ise/xj8fF6eFU
    !
    username admin privilege 15 secret 4 X4ZqtPJ///KxuEWxHSsJrv3beQVnz2ise/xj8fF6eFU
    no aaa new-model
    !
    ip cef
    !
    !
    no ip domain-lookup
    ip domain-name otus.ru
    no ipv6 cef
    ipv6 multicast rpf use-bgp
    !
    !
    !
    !
    !
    !
    !
    !
    spanning-tree mode rapid-pvst
    spanning-tree extend system-id
    spanning-tree vlan 1-4094 priority 61440
    !
    !
    !
    !
    vlan internal allocation policy ascending
    !
    ip ssh version 2
    !
    !
    !
    !
    !
    !
    !
    !
    !
    interface Loopback0
     ip address 10.255.255.3 255.255.255.255
    !
    interface Ethernet0/0
     description TO-SW4-E0/0
     switchport trunk encapsulation dot1q
     switchport trunk allowed vlan 10,999
     switchport mode trunk
     duplex auto
    !
    interface Ethernet0/1
     description TO-SW5-E0/1
     switchport trunk encapsulation dot1q
     switchport trunk allowed vlan 10,999
     switchport mode trunk
     duplex auto
    !
    interface Ethernet0/2
     description TO-VPC1
     switchport access vlan 10
     switchport mode access
     duplex auto
     spanning-tree portfast
    !
    interface Ethernet0/3
     duplex auto
    !
    interface Ethernet1/0
     duplex auto
    !
    interface Ethernet1/1
     duplex auto
    !
    interface Ethernet1/2
     duplex auto
    !
    interface Ethernet1/3
     duplex auto
    !
    interface Vlan999
     description MANAGEMENT
     ip address 10.255.254.3 255.255.255.0
     shutdown
    !
    ip default-gateway 10.255.254.254
    !
    no ip http server
    !
    !
    !
    !
    !
    control-plane
    !
    banner motd ^CSW3^C
    !
    line con 0
     exec-timeout 5 0
     logging synchronous
     login local
    line aux 0
    line vty 0 4
     exec-timeout 5 0
     logging synchronous
     login local
     transport input ssh
    !
    end
	
	SW3#show vlan brief
     VLAN Name                             Status    Ports
     ---- -------------------------------- --------- -------------------------------
     1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3
     10   VPC1                             active    Et0/2
     999  MANAGEMENT                       active
     1002 fddi-default                     act/unsup
     1003 token-ring-default               act/unsup
     1004 fddinet-default                  act/unsup
     1005 trnet-default                    act/unsup

	
	</details>    







