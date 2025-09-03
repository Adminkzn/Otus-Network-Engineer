#### Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах
##### Топология
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%204-1.jpg?raw=true)
##### Таблица адресации
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%204-2.jpg?raw=true)
#### Задачи:
##### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора

###### Шаг 1. Настройте маршрутизатор.
    Router>
    Router#conf t
    Router(config)#hostname R1
    R1(config)#service password-encryption 
    R1(config)#enable secret class
    R1(config)#banner motd #R1#
    R1(config)#line console 0
    R1(config-line)#logging synchronous 
    R1(config-line)#password cisco
    R1(config-line)#login
    R1(config-line)#exit
    R1(config)#interface gigabitEthernet 0/0/0
    R1(config-if)#no shutdown 
    R1(config-if)#exit
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#no
    R1(config-if)#no sh
    R1(config-if)#no shutdown 
    R1(config-if)#exit

######  Шаг 2. Настройте коммутатор.
    Switch>enable 
    Switch#conf t
    Switch(config)#hostname S1
    S1(config)#service password-encryption 
    S1(config)#enable secret class
    S1(config)#banner motd #S1#
    S1(config)#line console 0
    S1(config-line)#logging synchronous 
    S1(config-line)#password cisco
    S1(config-line)#login
    S1(config-line)#exit
    S1(config)#
##### Часть 2. Ручная настройка IPv6-адресов
###### Шаг 1. Назначьте IPv6-адреса интерфейсам Ethernet на R1.
    R1(config)#interface gigabitEthernet 0/0/0
    R1(config-if)#ipv6 address 2001:db8:acad:a::1/64
	R1(config-if)#ipv6 address fe80::1/64
    R1(config-if)#exit
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#ipv6 address 2001:db8:acad:1::1/64
	R1(config-if)#ipv6 address fe80::1/64
    R1(config-if)#exit
    R1(config)#exit 
    R1#
    R1#show ipv6 interface brief
    GigabitEthernet0/0/0       [up/up]
        FE80::202:4AFF:FEC6:1E01
        2001:DB8:ACAD:A::1
    GigabitEthernet0/0/1       [up/up]
        FE80::202:4AFF:FEC6:1E02
        2001:DB8:ACAD:1::1
    Vlan1                      [administratively down/down]
        unassigned
###### Какие группы многоадресной рассылки назначены интерфейсу G0/0?
    R1#show ipv6 interface GigabitEthernet0/0/0
    GigabitEthernet0/0/0 is up, line protocol is up
      IPv6 is enabled, link-local address is FE80::202:4AFF:FEC6:1E01
      No Virtual link-local address(es):
      Global unicast address(es):
        2001:DB8:ACAD:A::1, subnet is 2001:DB8:ACAD:A::/64
      Joined group address(es):
        FF02::1
        FF02::1:FF00:1
        FF02::1:FFC6:1E01
      MTU is 1500 bytes
      ICMP error messages limited to one every 100 milliseconds
      ICMP redirects are enabled
      ICMP unreachables are sent
      ND DAD is enabled, number of DAD attempts: 1
      ND reachable time is 30000 milliseconds
    R1#
###### Шаг 2. Активируйте IPv6-маршрутизацию на R1.

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%204-3.jpg?raw=true)

После выполнения команды IPv6 unicast-routing

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%204-4.jpg?raw=true)

###### Шаг 3. Назначьте IPv6-адреса интерфейсу управления (SVI) на S1.
###### Шаг 4. Назначьте компьютерам статические IPv6-адреса.

##### Часть 3. Проверка сквозного соединения

