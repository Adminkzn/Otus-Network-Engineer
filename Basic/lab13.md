![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-1.jpg?raw=true)
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-2.jpg?raw=true)

#### Часть 1. Создание сети и настройка основных параметров устройства
##### Шаг 1. Создайте сеть согласно топологии.
##### Шаг 2. Произведите базовую настройку маршрутизаторов.
###### Базовая настройка на примере R2
    Router>enable 
    Router#conf t
    Router(config)#hostname R2
    R2(config)#no ip domain-lookup 
    R2(config)#enable secret class
    R2(config)#line console 0
    R2(config-line)#password cisco
    R2(config-line)#login 
    R2(config-line)#exit
    R2(config)#line vty 0 4
    R2(config-line)#password cisco
    R2(config-line)#login
    R2(config-line)#exit
    R2(config)#service password-encryption 
    R2(config)#banner motd #!!!#
    R2(config)#ex
    R2#wr m
##### Шаг 3. Настройте базовые параметры каждого коммутатора.
###### Базовая настройка на примере S2
    Switch>enable 
    Switch#conf t 
    Switch(config)#hostname S2
    S2(config)#no ip domain-lookup 
    S2(config)#enable secret class
    S2(config)#line console 0
    S2(config-line)#password cisco
    S2(config-line)#login 
    S2(config-line)#exit
    S2(config)#line vty 0 4
    S2(config-line)#password class
    S2(config-line)#login 
    S2(config-line)#exit
    S2(config)#banner motd #!!!#
    S2(config)#service password-encryption 
    S2(config)#ex
    S2#wr m

#### Часть 2. Настройка сетей VLAN на коммутаторах.
##### Шаг 1. Создайте сети VLAN на коммутаторах.
##### a.	Создайте необходимые VLAN 
###### Настройка на S1
    S1#show vlan brief 
    
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                    Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                    Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                    Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                    Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                    Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                    Gig0/1, Gig0/2
    20   Management                       active    
    30   Operations                       active    
    40   Sales                            active    
    999  ParkingLot                       active    
    1000 Native                           active    
    1002 fddi-default                     active    
    1003 token-ring-default               active    
    1004 fddinet-default                  active    
    1005 trnet-default                    active    
	
###### Настройка на S2
    S2#show vlan brief 
    
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                    Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                    Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                    Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                    Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                    Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                    Gig0/1, Gig0/2
    20   Management                       active    
    30   Operations                       active    
    40   Sales                            active    
    999  ParkingLot                       active    
    1000 Native                           active    
    1002 fddi-default                     active    
    1003 token-ring-default               active    
    1004 fddinet-default                  active    
    1005 trnet-default                    active    

##### b.	Настрока интерфейса управления и шлюз по умолчанию на каждом коммутаторе
###### Настройка на S1
    S1(config)#interface vlan 20
    S1(config-if)#ip address 10.20.0.2 255.255.255.0
    S1(config-if)#no shutdown 
    S1(config-if)#ex
    S1(config)#ip default-gateway 10.20.0.1
    S1(config)#ex
    S1#wr m

###### Настройка на S2
    S2(config)#interface vlan 20
    S2(config-if)#ip address 10.20.0.3 255.255.255.0
    S2(config-if)#no shutdown 
    S2(config)#ip default-gateway 10.20.0.1
    S2(config)#ex
    S2#wr m

##### c.	Назначение VLAN ParkingLot и отключение интерфейсов
###### Настройка на S1
    S1(config)#interface range fastEthernet 0/2-4
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex
    S1(config)#interface range fastEthernet 0/7-24
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex
    S1(config)#interface range gigabitEthernet 0/1-2
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex

###### Настройка на S2
    S2(config)#interface range fastEthernet 0/2-4, fastEthernet 0/6-17, fastEthernet 0/19-24, gigabitEthernet 0/1-2
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
    S2(config-if-range)#shutdown 
    S2(config-if-range)#ex

##### Шаг 2. Назначение сети VLAN соответствующим интерфейсам коммутатора.
###### Настройка на S1
    S1(config-if)#switchport mode access 
    S1(config-if)#switchport access vlan 30
    S1(config-if)#description Operations
    S1(config-if)#ex
    S1(config)#ex
    S1#show vlan brief 
    
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/1, Fa0/5
    20   Management                       active    
    30   Operations                       active    Fa0/6
    40   Sales                            active    
    999  ParkingLot                       active    Fa0/2, Fa0/3, Fa0/4, Fa0/7
                                                    Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                    Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                    Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                    Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                    Fa0/24, Gig0/1, Gig0/2
    1000 Native                           active    
    1002 fddi-default                     active    
    1003 token-ring-default               active    
    1004 fddinet-default                  active    
    1005 trnet-default                    active    

###### Настройка на S2
	S2(config)#interface fastEthernet 0/18
    S2(config-if)#switchport mode access 
    S2(config-if)#switchport access vlan 40
    S2(config-if)#description Sales
    S2(config-if)#ex
    S2(config)#interface fastEthernet 0/5
    S2(config-if)#switchport mode access 
    S2(config-if)#switchport access vlan 20
    S2(config-if)#description Management
    S2(config-if)#ex
    S2(config)#ex
    S2#show vlan brief 
    
    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Fa0/1
    20   Management                       active    Fa0/5
    30   Operations                       active    
    40   Sales                            active    Fa0/18
    999  ParkingLot                       active    Fa0/2, Fa0/3, Fa0/4, Fa0/6
                                                    Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                    Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                    Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                    Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                    Fa0/24, Gig0/1, Gig0/2
    1000 Native                           active    
    1002 fddi-default                     active    
    1003 token-ring-default               active    
    1004 fddinet-default                  active    
    1005 trnet-default                    active

    
#### Часть 3. ·Настройте транки (магистральные каналы).
##### Шаг 1. Настройка F0/1.
###### Настройка на S1
    S1(config)#interface fastEthernet 0/1
    S1(config-if)#switchport mode trunk 
    S1(config-if)#switchport trunk allowed vlan 20,30,40,1000
    S1(config-if)#switchport trunk native vl
    S1(config-if)#switchport trunk native vlan 1000
    S1(config-if)#ex
    S1(config)#ex
    S1#show interfaces trunk 
    Port        Mode         Encapsulation  Status        Native vlan
    Fa0/1       on           802.1q         trunking      1000
    
    Port        Vlans allowed on trunk
    Fa0/1       20,30,40,1000
    
    Port        Vlans allowed and active in management domain
    Fa0/1       20,30,40,1000
    
    Port        Vlans in spanning tree forwarding state and not pruned
    Fa0/1       20,30,40

###### Настройка на S2
    
    S2(config)#interface fastEthernet 0/1
    S2(config-if)#switchport mode trunk 
    S2(config-if)#switchport trunk allowed vlan 20,30,40,1000
    S2(config-if)#switchport trunk native vlan 1000
    S2(config-if)#ex
    S2(config-if)#exit 
    S2(config)#ex
    S2#show interfaces trunk 
    Port        Mode         Encapsulation  Status        Native vlan
    Fa0/1       on           802.1q         trunking      1000
    
    Port        Vlans allowed on trunk
    Fa0/1       20,30,40,1000
    
    Port        Vlans allowed and active in management domain
    Fa0/1       20,30,40,1000
    
    Port        Vlans in spanning tree forwarding state and not pruned
    Fa0/1       20,30,40,1000

##### Шаг 2. Настройка F0/5 на коммутаторе S1.
###### Настройка на S1
    S1(config)#interface fastEthernet 0/5
    S1(config-if)#switchport mode trunk 
    switchport trunk allowed vlan 20,30,40,1000
    S1(config-if)#switchport trunk native vlan 1000
    S1(config-if)#description To-R1
    S1(config-if)#ex
    S1(config)#ex
    S1#show interfaces trunk 
    Port        Mode         Encapsulation  Status        Native vlan
    Fa0/1       on           802.1q         trunking      1000
    Fa0/5       on           802.1q         trunking      1000
    
    Port        Vlans allowed on trunk
    Fa0/1       20,30,40,1000
    Fa0/5       20,30,40,1000
    
    Port        Vlans allowed and active in management domain
    Fa0/1       20,30,40,1000
    Fa0/5       20,30,40,1000
    
    Port        Vlans in spanning tree forwarding state and not pruned
    Fa0/1       20,30,40,1000
    Fa0/5       20,30,40,1000
    
	
#### Часть 4. Настройте маршрутизацию.
##### Шаг 1. Настройка маршрутизации между сетями VLAN на R1.
###### Настройка на R1
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#no shutdown 
    R1(config-if)#ex
    R1(config)#interface gigabitEthernet 0/0/1.20
    R1(config-subif)#encapsulation dot1Q 20
    R1(config-subif)#ip address 10.20.0.1 255.255.255.0
    R1(config-subif)#description Management VLAN
    R1(config-subif)#ex
    R1(config)#interface gigabitEthernet 0/0/1.30
    R1(config-subif)#encapsulation dot1Q 30
    R1(config-subif)#ip address 10.30.0.1 255.255.255.0
    R1(config-subif)#description Operations VLAN
    R1(config-subif)#ex
    R1(config)#interface gigabitEthernet 0/0/1.40
    R1(config-subif)#encapsulation dot1Q 40
    R1(config-subif)#ip address 10.40.0.1 255.255.255.0
    R1(config-subif)#description Sales VLAN
    R1(config-subif)#ex
    R1(config)#interface gigabitEthernet 0/0/1.1000
    R1(config-subif)#encapsulation dot1Q 1000 native
    R1(config-subif)#description Native VLAN
    R1(config-subif)#ex
    R1(config)#interface loopback1
    R1(config-if)#ip address 172.16.1.1 255.255.255.0
    R1(config-if)#no shutdown 
    R1(config-if)#ex
	R1(config)#ex
    R1#wr m
    
##### Шаг 2. Настройка интерфейса R2 g0/0/1 с использованием адреса из таблицы и маршрута по умолчанию с адресом следующего перехода 10.20.0.1
###### Настройка на R2
    R2(config)#interface gigabitEthernet 0/0/1
    R2(config-if)#ip address 10.20.0.4 255.255.255.0
    R2(config-if)#no shutdown
    R2(config-if)#ex
    R2(config)#ip route 0.0.0.0 0.0.0.0 10.20.0.1
    R2(config)#ex
    R2#wr m

#### Часть 5. Настройте удаленный доступ
##### Шаг 1. Настройте все сетевые устройства для базовой поддержки SSH.
###### Настройка на примере R1
    R1(config)#username SSHadmin privilege 15 secret $cisco123!
    R1(config)#ip domain-name ccna-lab.com
    R1(config)#crypto key generate rsa
    R1(config)#line vty 0 4
    R1(config-line)#transport input ssh
    R1(config-line)#login local
    R1(config-line)#end
    R1#wr m

##### Шаг 2. Включите защищенные веб-службы с проверкой подлинности на R1.
###### ???

#### Часть 6. Проверка подключения
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-3.jpg?raw=true)
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-4.jpg?raw=true)
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-5.jpg?raw=true)
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-6.jpg?raw=true)
#### Часть 7. Настройка и проверка списков контроля доступа (ACL)
###### Настройка на R1
    R1(config)#ip access-list extended SALES-ACL
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255 eq 22
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255 eq 80
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255 eq 443
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 host 10.20.0.1 eq 443
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 host 10.20.0.1 eq 80
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 host 10.30.0.1 eq 443
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 host 10.30.0.1 eq 80
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 host 10.40.0.1 eq 443
    R1(config-ext-nacl)#deny tcp 10.40.0.0 0.0.0.255 host 10.40.0.1 eq 80
    R1(config-ext-nacl)#permit tcp 10.40.0.0 0.0.0.255 host 172.16.1.1 eq 443
    R1(config-ext-nacl)#deny ic 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255
    R1(config-ext-nacl)#deny icmp 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255
    R1(config-ext-nacl)#deny icmp 10.40.0.0 0.0.0.255 10.30.0.0 0.0.0.255
    R1(config-ext-nacl)#permit ip any any 
    R1(config-ext-nacl)#ex
    R1(config)#interface gigabitEthernet 0/0/1.40
    R1(config-subif)#ip access-group SALES-ACL in
    R1(config-subif)#ex
    R1(config)#ip access-list extended OPERATIONS-ACL
    R1(config-ext-nacl)#deny icmp 10.30.0.0 0.0.0.255 10.40.0.0 0.0.0.255
    R1(config-ext-nacl)#permit ip any any 
    R1(config-ext-nacl)#ex
    R1(config)#interface gigabitEthernet 0/0/1.30
    R1(config-subif)#ip access-group OPERATIONS-ACL in 
    R1(config-subif)#ex
    R1(config)#ex
    wr m
##### Проверка
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2013-7.jpg?raw=true)

