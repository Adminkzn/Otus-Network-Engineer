![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-1.jpg?raw=true)
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-2.jpg?raw=true)

### Часть 1. Настройка основного сетевого устройства
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-3.jpg?raw=true)
###### Настройте маршрутизатор R1
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
	
###### show ip interface brief
    R1#show ip interface brief
    Interface              IP-Address      OK? Method Status                Protocol 
    GigabitEthernet0/0/0   unassigned      YES unset  administratively down down 
    GigabitEthernet0/0/1   192.168.10.1    YES manual up                    up 
    GigabitEthernet0/0/2   unassigned      YES unset  administratively down down 
    Loopback0              10.10.1.1       YES manual up                    up 
    Vlan1                  unassigned      YES unset  administratively down down

#### Шаг 3. Настройка и проверка основных параметров коммутатора
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
######  S1:
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

#### Часть 3. Настройки безопасности коммутатора.
######  S1:
	S1(config)#interface range fastEthernet 0/5, fastEthernet 0/6
	S1(config-if-range)#switchport mode access 
	S1(config-if-range)#switchport access vlan 10
	S1(config-if-range)#ex
    S1(config)#interface fastEthernet 0/1
    S1(config-if)#switchport mode trunk 
    S1(config-if)#switchport trunk native vlan 333
    S1(config-if)#switchport nonegotiate 
	S1(config-if)#ex
	S1(config)#interface range fastEthernet 0/2-4
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#interface range fastEthernet 0/7-24
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex
    S1(config)#interface gigabitEthernet 0/1
    S1(config-if)#switchport mode access 
    S1(config-if)#switchport access vlan 999
    S1(config-if)#shutdown 
    S1(config-if)#ex
    S1(config)#interface gigabitEthernet 0/2
    S1(config-if)#switchport mode access 
    S1(config-if)#switchport access vlan 999
    S1(config-if)#shutdown 
######  show interfaces status S1:
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-4.jpg?raw=true)
######  show interfaces status S2:
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-9.jpg?raw=true)

#### Шаг 4. Документирование и реализация функций безопасности порта.
###### S1:
    S1(config)#interface fastEthernet 0/6
    S1(config-if)#switchport port-security 
    S1(config-if)#switchport port-security maximum 3
    S1(config-if)#switchport port-security violation restrict 
    S1(config-if)#switchport port-security aging time 60
    
###### S1:
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-6.jpg?raw=true)
###### S2:
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-7.jpg?raw=true)

#### Шаг 5. Реализовать безопасность DHCP snooping.

    S2(config)#ip dhcp snooping 
    S2(config)#ip dhcp snooping vlan 10
    S2(config)#interface fastEthernet 0/1
    S2(config-if)#ip dhcp snooping trust 
    S2(config-if)#ex
    S2(config)#interface fastEthernet 0/18
    S2(config-if)#ip dhcp snooping limit rate 5
    S2(config-if)#ex
	S2(config)#no ip dhcp snooping information option

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-10.jpg?raw=true)

#### Шаг 6. Реализация PortFast и BPDU Guard
###### S1
    S1(config)#interface fastEthernet 0/6
    S1(config-if)#spanning-tree portfast 
    S1(config-if)#spanning-tree bpduguard enable 
    S1(config-if)#ex

#### Шаг 7. Проверьте наличие сквозного ⁪подключения.
###### PC-B
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2011-11.jpg?raw=true)


