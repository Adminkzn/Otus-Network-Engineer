## Домашнее задание №1
#### Проектирование сети

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/Pro/Lab1/img/1.jpg?raw=true)

Цель:
распланировать адресное пространство, настроить IP на активных портах для дальнейшей работы над проектом и задокументировать адресацию.

------------

#### Разработаете и задокументируете адресное пространство для лабораторного стенда.

#### 1. Management VLAN

| SW | Interface | IP Address    |
|---------|-----------|---------------|
| SW2     | VLAN 99   | 192.168.99.2/24  |
| SW3     | VLAN 99   | 192.168.99.3/24  |
| SW4     | VLAN 99   | 192.168.99.4/24  |
| SW5     | VLAN 99   | 192.168.99.5/24  |
| SW9     | VLAN 99   | 192.168.99.9/24  |
| SW10    | VLAN 99   | 192.168.99.10/24 |
| SW29    | VLAN 99   | 192.168.99.29/24 |


#### 2. Loopback маршрутизаторов

| R | Interface | IP Address     |
|---------|-----------|----------------|
| R12     | Lo0       | 10.255.0.12/32 |
| R13     | Lo0       | 10.255.0.13/32 |
| R14     | Lo0       | 10.255.0.14/32 |
| R15     | Lo0       | 10.255.0.15/32 |
| R16     | Lo0       | 10.255.0.16/32 |
| R17     | Lo0       | 10.255.0.17/32 |
| R18     | Lo0       | 10.255.0.18/32 |
| R19     | Lo0       | 10.255.0.19/32 |
| R20     | Lo0       | 10.255.0.20/32 |
| R21     | Lo0       | 10.255.0.21/32 |
| R22     | Lo0       | 10.255.0.22/32 |
| R23     | Lo0       | 10.255.0.23/32 |
| R24     | Lo0       | 10.255.0.24/32 |
| R25     | Lo0       | 10.255.0.25/32 |
| R26     | Lo0       | 10.255.0.26/32 |
| R27     | Lo0       | 10.255.0.27/32 |
| R28     | Lo0       | 10.255.0.28/32 |
| R32     | Lo0       | 10.255.0.32/32 |

#### 2. Пользовательские VLAN
| Офис            | VLAN | Network         | Gateway        |
|-----------------|-----:|-----------------|----------------|
| Москва          | 10   | 192.168.10.0/24 | 192.168.10.1   |
| Санкт-Петербург | 20   | 192.168.20.0/24 | 192.168.20.1   |
| Чокурдах        | 30   | 192.168.30.0/24 | 192.168.30.1   |













------------

















#### 2. Клиентские LAN-сегменты
|  Устройство | Vlan |  IP-Адрес | Шлюз | Коментарий |
| ------------ | ------------ |------------ |------------ | ------------ |
|  VPC1 |10|10.10.10.10/24| R12/13 10.10.10.254/24 || 
|  VPC7 |70|10.10.70.10/24|R12/13 10.10.70.254/24|| 
|  VPC6 |60|||| 
|  VPC8 |80|||| 
|  VPC30 |300|||| 
|  VPC31 |310||||| 

#### 3. Межвлановая смаршрутизация 
|  Устройство | VLAN10 |  VLAN70 | Коментарий |
| ------------ | ------------ |------------ | ------------ |
|  R12 | 10.10.10.253/24 | 10.10.70.253/24 | priority 150 vrrp 70 ip 10.10.70.254, vrrp 10 ip 10.10.10.254 |
|  R13 | 10.10.10.252/24 | 10.10.70.252/24 | priority 200 vrrp 70 ip 10.10.70.254, vrrp 10 ip 10.10.10.254 |
|  R14 | 10.255.254.14/24 |10.255.255.14/32||
|  R15 | 10.255.254.15/24 |10.255.255.15/32||
|  R16 | 10.255.254.16/24 |10.255.255.16/32||
|  R17 | 10.255.254.17/24 |10.255.255.17/32||
|  R18 | 10.255.254.18/24 |10.255.255.18/32||
|  R19 | 10.255.254.19/24 |10.255.255.19/32||
|  R20 | 10.255.254.20/24 |10.255.255.20/32||
|  R21 | 10.255.254.21/24 |10.255.255.21/32||
|  R22 | |10.255.255.22/32||
|  R23 |  |10.255.255.23/32||
|  R24 | |10.255.255.24/32||
|  R25 |  |10.255.255.25/32||
|  R26 |  |10.255.255.26/32||
|  R27 |  |10.255.255.27/32||
|  R28 |  |10.255.255.28/32||
|  R32 |   |||

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

------------


#### Настройка SW2
<details>

	SW2#show running-config
	Building configuration...
	
	Current configuration : 1933 bytes
	!
	! Last configuration change at 05:37:42 UTC Fri May 29 2026 by admin
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
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/0
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/1
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/2
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/3
	 description UNUSED
	 shutdown
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

	SW2#sh
	SW2#show vlan
	
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
	
	VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
	---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
	1    enet  100001     1500  -      -      -        -    -        0      0
	70   enet  100070     1500  -      -      -        -    -        0      0
	999  enet  100999     1500  -      -      -        -    -        0      0
	1002 fddi  101002     1500  -      -      -        -    -        0      0
	1003 tr    101003     1500  -      -      -        -    -        0      0
	1004 fdnet 101004     1500  -      -      -        ieee -        0      0
	1005 trnet 101005     1500  -      -      -        ibm  -        0      0

	Primary Secondary Type              Ports
	------- --------- ----------------- ------------------------------------------

</details>

#### Настройка SW3
<details>
	
	SW3#show running-config
	Building configuration...

	Current configuration : 1933 bytes
	!
	! Last configuration change at 05:32:14 UTC Fri May 29 2026 by admin
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
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/0
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/1
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/2
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/3
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Vlan999
	 description MANAGEMENT
	 ip address 10.255.254.3 255.255.255.0
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

	SW3#show vlan
	
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
	
	VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
	---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
	1    enet  100001     1500  -      -      -        -    -        0      0
	10   enet  100010     1500  -      -      -        -    -        0      0
	999  enet  100999     1500  -      -      -        -    -        0      0
	1002 fddi  101002     1500  -      -      -        -    -        0      0
	1003 tr    101003     1500  -      -      -        -    -        0      0
	1004 fdnet 101004     1500  -      -      -        ieee -        0      0
	1005 trnet 101005     1500  -      -      -        ibm  -        0      0
	
	Primary Secondary Type              Ports
	------- --------- ----------------- ------------------------------------------
	
</details>

#### Настройка SW4
<details>
	
	SW4#show running-config
	Building configuration...
	
	Current configuration : 2246 bytes
	!
	! Last configuration change at 10:53:03 UTC Thu May 28 2026
	!
	version 15.1
	service timestamps debug datetime msec
	service timestamps log datetime msec
	service password-encryption
	service compress-config
	!
	hostname SW4
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
	spanning-tree vlan 1-4094 priority 28672
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
	 ip address 10.255.255.4 255.255.255.255
	!
	interface Port-channel1
	 switchport
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,70,999
	 switchport mode trunk
	!
	interface Ethernet0/0
	 description TO-SW3-E0/0
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,999
	 switchport mode trunk
	 duplex auto
	!
	interface Ethernet0/1
	 description TO-SW2-E0/1
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 70,999
	 switchport mode trunk
	 duplex auto
	!
	interface Ethernet0/2
	 description TO-SW5-PORTCHANNEL
 	switchport trunk encapsulation dot1q
 	switchport trunk allowed vlan 10,70,999
 	switchport mode trunk
 	duplex auto
 	channel-group 1 mode active
	!
	interface Ethernet0/3
	 description TO-SW5-PORTCHANNEL
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,70,999
	 switchport mode trunk
	 duplex auto
	 channel-group 1 mode active
	!
	interface Ethernet1/0
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/1
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/2
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/3
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Vlan999
	 description MANAGEMENT
	 ip address 10.255.254.4 255.255.255.0
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
	
	SW4#show vlan
	
	VLAN Name                             Status    Ports
	---- -------------------------------- --------- -------------------------------
	1    default                          active    Et1/0, Et1/1, Et1/2, Et1/3
	10   VPC1                             active
	70   VPC7                             active
	999  MANAGEMENT                       active
	1002 fddi-default                     act/unsup
	1003 token-ring-default               act/unsup
	1004 fddinet-default                  act/unsup
	1005 trnet-default                    act/unsup

	VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
	---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
	1    enet  100001     1500  -      -      -        -    -        0      0
	10   enet  100010     1500  -      -      -        -    -        0      0
	70   enet  100070     1500  -      -      -        -    -        0      0
	999  enet  100999     1500  -      -      -        -    -        0      0
	1002 fddi  101002     1500  -      -      -        -    -        0      0
	1003 tr    101003     1500  -      -      -        -    -        0      0
	1004 fdnet 101004     1500  -      -      -        ieee -        0      0
	1005 trnet 101005     1500  -      -      -        ibm  -        0      0
	
	Primary Secondary Type              Ports
	------- --------- ----------------- ------------------------------------------

</details>

#### Настройка SW5


<details>
	
	SW5#show running-config
	Building configuration...
	
	Current configuration : 2273 bytes
	!
	! Last configuration change at 05:28:28 UTC Fri May 29 2026 by admin
	!
	version 15.1
	service timestamps debug datetime msec
	service timestamps log datetime msec
	service password-encryption
	service compress-config
	!
	hostname SW5
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
	spanning-tree vlan 1-4094 priority 28672
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
	 ip address 10.255.255.5 255.255.255.255
	!
	interface Port-channel1
	 switchport
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,70,999
	 switchport mode trunk
	!
	interface Ethernet0/0
	 description TO-SW2-E0/0
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 70,999
	 switchport mode trunk
	 duplex auto
	!
	interface Ethernet0/1
	 description TO-SW3-E0/1
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,999
	 switchport mode trunk
	 duplex auto
	!
	interface Ethernet0/2
	 description TO-SW4-PORTCHANNEL
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,70,999
	 switchport mode trunk
	 duplex auto
	 channel-group 1 mode active
	!
	interface Ethernet0/3
	 description TO-SW4-PORTCHANNEL
	 switchport trunk encapsulation dot1q
	 switchport trunk allowed vlan 10,70,999
	 switchport mode trunk
	 duplex auto
	 channel-group 1 mode active
	!
	interface Ethernet1/0
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/1
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/2
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Ethernet1/3
	 description UNUSED
	 shutdown
	 duplex auto
	!
	interface Vlan999
	 description MANAGEMENT
	 ip address 10.255.254.5 255.255.255.0
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
	banner motd ^CSW5^C
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
	
	SW5#show vlan
	
	VLAN Name                             Status    Ports
	---- -------------------------------- --------- -------------------------------
	1    default                          active    Et1/0, Et1/1, Et1/2, Et1/3
	10   VPC1                             active
	70   VPC7                             active
	999  MANAGEMENT                       active
	1002 fddi-default                     act/unsup
	1003 token-ring-default               act/unsup
	1004 fddinet-default                  act/unsup
	1005 trnet-default                    act/unsup

	VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
	---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
	1    enet  100001     1500  -      -      -        -    -        0      0
	10   enet  100010     1500  -      -      -        -    -        0      0
	70   enet  100070     1500  -      -      -        -    -        0      0
	999  enet  100999     1500  -      -      -        -    -        0      0
	1002 fddi  101002     1500  -      -      -        -    -        0      0
	1003 tr    101003     1500  -      -      -        -    -        0      0
	1004 fdnet 101004     1500  -      -      -        ieee -        0      0
	1005 trnet 101005     1500  -      -      -        ibm  -        0      0
	
	Primary Secondary Type              Ports
	------- --------- ----------------- ------------------------------------------
	
</details>








