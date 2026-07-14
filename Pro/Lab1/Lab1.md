## Домашнее задание №1
#### Проектирование сети

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/Pro/Lab1/img/1.jpg?raw=true)

Цель:
распланировать адресное пространство, настроить IP на активных портах для дальнейшей работы над проектом и задокументировать адресацию.

------------

#### Разработаете и задокументируете адресное пространство для лабораторного стенда.

#### 1. Management VLAN коммутаторов 

| SW | Interface | IP Address    |
|---------|-----------|---------------|
| SW2     | VLAN 99   | 192.168.100.2/24  |
| SW3     | VLAN 99   | 192.168.100.3/24  |
| SW4     | VLAN 99   | 192.168.100.4/24  |
| SW5     | VLAN 99   | 192.168.100.5/24  |
| SW9     | VLAN 99   | 192.168.101.9/24  |
| SW10    | VLAN 99   | 192.168.101.10/24 |
| SW29    | VLAN 99   | 192.168.102.29/24 |

R12	192.168.100.1/24
R17	192.168.101.1/24
R28	192.168.102.1/24



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


#### 3. Пользовательские VLAN
| Офис            | VLAN | Network         | Gateway        |
|-----------------|-----:|-----------------|----------------|
| Москва          | 10   | 192.168.10.0/24 | 192.168.10.1   |
| Санкт-Петербург | 20   | 192.168.20.0/24 | 192.168.20.1   |
| Чокурдах        | 30   | 192.168.30.0/24 | 192.168.30.1   |


#### 4. Адрессация компьютеров
| Device | VLAN | IP Address      | Gateway      |
|--------|-----:|-----------------|--------------|
| VPC1   | 10   | 192.168.10.10   | 192.168.10.1 |
| VPC7   | 10   | 192.168.10.11   | 192.168.10.1 |
| VPC8   | 20   | 192.168.20.10   | 192.168.20.1 |
| VPC    | 20   | 192.168.20.11   | 192.168.20.1 |
| VPC30  | 30   | 192.168.30.10   | 192.168.30.1 |
| VPC31  | 30   | 192.168.30.11   | 192.168.30.1 |


#### 5. Соединения между маршрутизаторами

| Router A - Router B | Network       | Router A | Router B |
|------------|---------------|----------|----------|
| R12-R14 | 10.0.0.0/30  | 10.0.0.1 | 10.0.0.2 |
| R13-R15 | 10.0.0.4/30  | 10.0.0.5 | 10.0.0.6 |
| R13-R14 | 10.0.0.8/30  | 10.0.0.9 | 10.0.0.10 |
| R12-R15 | 10.0.0.12/30 | 10.0.0.13 | 10.0.0.14 |
| R14-R22 | 10.0.0.16/30 | 10.0.0.17 | 10.0.0.18 |
| R15-R21 | 10.0.0.20/30 | 10.0.0.21 | 10.0.0.22 |
| R21-R22 | 10.0.0.24/30 | 10.0.0.25 | 10.0.0.26 |
| R22-R23 | 10.0.0.28/30 | 10.0.0.29 | 10.0.0.30 |
| R21-R24 | 10.0.0.32/30 | 10.0.0.33 | 10.0.0.34 |
| R23-R25 | 10.0.0.36/30 | 10.0.0.37 | 10.0.0.38 |
| R24-R26 | 10.0.0.40/30 | 10.0.0.41 | 10.0.0.42 |
| R25-R27 | 10.0.0.44/30 | 10.0.0.45 | 10.0.0.46 |
| R26-R28 | 10.0.0.48/30 | 10.0.0.49 | 10.0.0.50 |
| R25-R26 | 10.0.0.52/30 | 10.0.0.53 | 10.0.0.54 |
| R23-R24 | 10.0.0.56/30 | 10.0.0.57 | 10.0.0.58 |
| R18-R24 | 10.0.0.60/30 | 10.0.0.61 | 10.0.0.62 |
| R18-R26 | 10.0.0.64/30 | 10.0.0.65 | 10.0.0.66 |
| R25-R28 | 10.0.0.68/30 | 10.0.0.69 | 10.0.0.70 |
| R15-R20 | 10.0.0.72/30 | 10.0.0.73 | 10.0.0.74 |
| R14-R19 | 10.0.0.76/30 | 10.0.0.77 | 10.0.0.78 |
| R16-R18 | 10.0.0.80/30 | 10.0.0.81 | 10.0.0.82 |
| R17-R18 | 10.0.0.84/30 | 10.0.0.85 | 10.0.0.86 |
| R16-R32 | 10.0.0.88/30 | 10.0.0.89 | 10.0.0.90 |
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








