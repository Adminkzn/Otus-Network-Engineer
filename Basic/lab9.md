![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%208-5.jpg?raw=true)

### Шаг 1. Создайте сеть согласно топологии.

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%208-6.jpg?raw=true)

### Шаг 3. Произведите базовую настройку маршрутизаторов.

#### R1
    Router(config)#hostname R1
    R1(config)#no ip domain-lookup 
    R1(config)#ipv6 unicast-routing 
#### R2
    Router(config)#hostname R2
    R2(config)#no ip domain-lookup 
    R2(config)#ipv6 unicast-routing

### Шаг 4. Настройка интерфейсов и маршрутизации для обоих маршрутизаторов.

#### R1

    R1(config)#interface gigabitEthernet 0/0/0
    R1(config-if)#ipv6 address 2001:db8:acad:2::1/64
    R1(config-if)#ipv6 address fe80::1 link-local 
	R1(config-if)#no shutdown
    R1(config-if)#exit 
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#ipv6 address 2001:db8:acad:1::1/64
    R1(config-if)#ipv6 address fe80::1 link-local 
	R1(config-if)#no shutdown
    R1(config-if)#exit 
    R1(config)#ipv6 route ::/0 2001:db8:acad:2::2

#### R2

    R2(config)#interface gigabitEthernet 0/0/0
    R2(config-if)#no SHutdown 
    R2(config-if)#ipv6 address 2001:db8:acad:2::2/64
    R2(config-if)#ipv6 address fe80::2 link-local 
    R2(config-if)#exit 
    R2(config)#interface gigabitEthernet 0/0/1
    R2(config-if)#no shutdown 
    R2(config-if)#ipv6 address 2001:db8:acad:3::1/64
    R2(config-if)#ipv6 address fe80::1 link-local 
    R2(config-if)#exit 
    R2(config)#ipv6 route ::/0 2001:db8:acad:2::1
    R2#copy running-config startup-config 
    
#### R1 ping R2
    	
    R1#ping 2001:db8:acad:2::2
    
    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 2001:db8:acad:2::2, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms
    
    R1#ping 2001:db8:acad:3::1
    
    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 2001:db8:acad:3::1, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms
	

### Часть 2. Проверка назначения адреса SLAAC от R1

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%208-7.jpg?raw=true)

Откуда взялась часть адреса с идентификатором хоста?
Сгенерировался на основе мак адреса 

### Шаг 2. Настройте R1 для предоставления DHCPv6 без состояния для PC-A.

    R1(config)#ipv6 dhcp pool R1-STATELESS
    R1(config-dhcpv6)#dns-server 2001:db8:acad::254
    R1(config-dhcpv6)#domain-name STATELESS.com
    R1(config-dhcpv6)#exit
    R1(config)#interface g0/0/1
    R1(config-if)#ipv6 nd other-config-flag 
    R1(config-if)#ipv6 dhcp server R1-STATELESS

### Часть 4. Настройка сервера DHCPv6 с сохранением состояния на R1

    R1(config)#ipv6 dhcp pool R2-STATEFUL
    R1(config-dhcpv6)#address prefix 2001:db8:acad:3:aaa::/80
    R1(config-dhcpv6)#dns-server 2001:db8:acad::254
    R1(config-dhcpv6)#domain-name STATEFUL.com
    R1(config-dhcpv6)#exit 
    R1(config)#interface g0/0/0
    R1(config-if)#ipv6 dhcp server R2-STATEFUL
    R1(config-if)#exit 
	
### Часть 5. Настройка и проверка ретрансляции DHCPv6 на R2.

    R2(config)#ipv6 dhcp pool PC-B
    R2(config-dhcpv6)#dns-server 2001:db8:acad:3::1
	R2(config-dhcpv6)#address prefix 2001:db8:acad:3::/64
    R2(config-dhcpv6)#exit 
    R2(config)#interface gigabitEthernet 0/0/1
    R2(config-if)#ipv6 nd managed-config-flag 
    R2(config-if)#ipv6 dhcp server PC-B
    R2(config-if)#exit
    R2(config)#
	

### PC-B пингует PC-A











