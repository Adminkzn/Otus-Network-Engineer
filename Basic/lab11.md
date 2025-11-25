![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-1.jpg?raw=true)
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-2.jpg?raw=true)

### Часть 1. Настройка основного сетевого устройства
#### Шаг 1. Создайте сеть.
##### a.	Создайте сеть согласно топологии.
##### b.	Инициализация устройств
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-3.jpg?raw=true)

#### Шаг 2. Настройте маршрутизатор R1.
##### a.	Загрузите следующий конфигурационный скрипт на R1.
    R1#show running-config 
    Building configuration...
    
    Current configuration : 1022 bytes
    !
    version 16.6.4
    no service timestamps log datetime msec
    no service timestamps debug datetime msec
    no service password-encryption
    !
    hostname R1
    !
    !
    !
    !
    ip dhcp excluded-address 192.168.10.1 192.168.10.9
    ip dhcp excluded-address 192.168.10.201 192.168.10.202
    !
    ip dhcp pool Students
     network 192.168.10.0 255.255.255.0
     default-router 192.168.10.1
     domain-name CCNA2.Lab-11.6.1
    !
    !
    !
    ip cef
    no ipv6 cef
    !
    !
    !
    !
    !
    !
    !
    !
    !
    !
    no ip domain-lookup
    !
    !
    spanning-tree mode pvst
    !
    !
    !
    !
    !
    !
    interface Loopback0
     ip address 10.10.1.1 255.255.255.0
    !
    interface GigabitEthernet0/0/0
     no ip address
     duplex auto
     speed auto
     shutdown
    !
    interface GigabitEthernet0/0/1
     description Link to S1
     ip address 192.168.10.1 255.255.255.0
     duplex auto
     speed auto
    !
    interface GigabitEthernet0/0/2
     no ip address
     duplex auto
     speed auto
     shutdown
    !
    interface Vlan1
     no ip address
     shutdown
    !
    ip classless
    !
    ip flow-export version 9
    !
    !
    !
    !
    !
    !
    !
    !
    line con 0
     exec-timeout 0 0
     logging synchronous
    !
    line aux 0
    !
    line vty 0 4
     login
    !
    !
    !
    end
	
##### b.	Проверьте текущую конфигурацию на R1, используя следующую команду: R1# show ip interface brief
##### c.	Убедитесь, что IP-адресация и интерфейсы находятся в состоянии up / up (при необходимости устраните неполадки).
    R1#show ip interface brief
    Interface              IP-Address      OK? Method Status                Protocol 
    GigabitEthernet0/0/0   unassigned      YES unset  administratively down down 
    GigabitEthernet0/0/1   192.168.10.1    YES manual up                    up 
    GigabitEthernet0/0/2   unassigned      YES unset  administratively down down 
    Loopback0              10.10.1.1       YES manual up                    up 
    Vlan1                  unassigned      YES unset  administratively down down

#### Шаг 3. Настройка и проверка основных параметров коммутатора
##### a.	Настройте имя хоста для коммутаторов S1 и S2.
##### Откройте окно конфигурации
##### b.	Запретите нежелательный поиск в DNS.
##### c.	Настройте описания интерфейса для портов, которые используются в S1 и S2.
##### d.	Установите для шлюза по умолчанию для VLAN управления значение 192.168.10.1 на обоих коммутаторах.
######    S1
   S1(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#ip default-gateway 192.168.10.1
    S1(config)#interface fastEthernet 0/5
    S1(config-if)#description R1
    S1(config-if)#ex
    S1(config)#interface fastEthernet 0/1
    S1(config-if)#description S2
    S1(config-if)#ex
    S1(config)#interface fastEthernet 0/6
    S1(config-if)#description PC-A
    S1(config-if)#ex

#### Часть 2. Настройка сетей VLAN на коммутаторах.
##### Шаг 1. Сконфигруриуйте VLAN 10.
###### Добавьте VLAN 10 на S1 и S2 и назовите VLAN - Management.
##### Шаг 2. Сконфигруриуйте SVI для VLAN 10.
###### Настройте IP-адрес в соответствии с таблицей адресации для SVI для VLAN 10 на S1 и S2. Включите интерфейсы SVI и предоставьте описание для интерфейса.
##### Шаг 3. Настройте VLAN 333 с именем Native на S1 и S2.Шаг 3. 
##### Шаг 4. Настройте VLAN 999 с именем ParkingLot на S1 и S2.
###### S1:
    S1(config-if)#vlan 10
    S1(config-vlan)#name Management
    S1(config-vlan)#ex
    S1(config)#vlan 333
    S1(config-vlan)#name Native
    S1(config-vlan)#ex
    S1(config)#vlan
    S1(config)#vlan 999
    S1(config-vlan)#name ParkingLot
    S1(config-vlan)#ex
    S1(config)#interface vlan 10
    S1(config-if)#
    %LINK-5-CHANGED: Interface Vlan10, changed state to up
    S1(config-if)#ip address 192.168.10.201 255.255.255.0
    S1(config-if)#description Management vlan
    S1(config-if)#ex
    S1(config)#interface vlan 333
    %LINK-5-CHANGED: Interface Vlan333, changed state to up
    S1(config-if)#ex
    S1(config)#interface vlan 999
    %LINK-5-CHANGED: Interface Vlan999, changed state to up
    S1(config-if)#ex



