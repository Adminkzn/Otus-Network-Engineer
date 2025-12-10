![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2012-1.jpg?raw=true)
#### Часть 1. Создание сети и настройка основных параметров устройства
##### Шаг 1. Создайте сеть согласно топологии.

##### Шаг 2. Произведите базовую настройку маршрутизаторов.
###### Настройка на примере R1
    Router>enable
    Router#configure t
    Router(config)#hostname R1
    R1(config)#no ip domain-lookup 
    R1(config)#banner motd #!!!#
    R1(config)#service password-encryption 
    R1(config)#line console 0
    R1(config-line)#password cisco
    R1(config-line)#login
    R1(config-line)#exit
    R1(config)#line vty 0 4
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#exit
    R1(config)#enable secret class
    R1(config)#ex
    R1#write m
##### Шаг 3. Настройте базовые параметры каждого коммутатора.
###### Настройка на примере S1
    Switch>enable 
    Switch#conf t
    Switch(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#banner motd #!!!#
    S1(config)#service password-encryption 
    S1(config)#line console 0
    S1(config-line)#password cisco
    S1(config-line)#login
    S1(config-line)#exit
    S1(config)#line vty 0 4
    S1(config-line)#password cisco
    S1(config-line)#login
    S1(config-line)#exit
    S1(config)#en
    S1(config)#enable password class
    S1(config)#ex
    S1#wr m
#### Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области
##### Шаг 1. Настройте адреса интерфейса и базового OSPFv2 на каждом маршрутизаторе.
###### Настройка и проверка адрессации на примере R2
    R2(config)#interface g 0/0/1
    R2(config-if)#ip address 10.53.0.2 255.255.255.0
    R2(config-if)#no shutdown 
    R2(config-if)#ex
    R2(config)#interface loopback 1
    R2(config-if)#ip address 192.168.1.1 255.255.255.0
    R2(config-if)#no shutdown 
    R2(config-if)#ex
    R2(config)#ex
    R2#ping 10.53.0.1
    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 10.53.0.1, timeout is 2 seconds:
    .!!!!
    Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms
    R2#ping 10.53.0.1
    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 10.53.0.1, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/1 ms
    
###### Настройка и проверка OSPF на примере R2
    R2(config)#router ospf 56
    R2(config-router)#router-id 2.2.2.2
    R2(config-router)#network 10.53.0.0 0.0.0.255 area 0
    R2(config-router)#network 192.168.1.0 0.0.0.255 area 0
    R2(config-router)#ex
    R2(config)#ex
    R2#wr m
    R2#show ip ospf neighbor 
    Neighbor ID     Pri   State           Dead Time   Address         Interface
    1.1.1.1           1   FULL/BDR        00:00:34    10.53.0.1      
#### Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области
##### Шаг 1. Реализация различных оптимизаций на каждом маршрутизаторе.
###### Настройка R1
    R1(config)#interface g 0/0/1
    R1(config-if)#ip ospf priority 50
	R1(config-if)#ip ospf hello-interval 30
    R1(config-if)#ip ospf dead-interval 120
    R1(config-if)#ex
    R1(config)#ip route 0.0.0.0 0.0.0.0 loopback 1
	R1(config)#router ospf 56
    R1(config-router)#default-information originate 
	R1(config-router)#auto-cost reference-bandwidth 1000
    R1(config-router)#ex
    R1(config)#ex
	
###### Настройка R2
    R2(config)#interface g 0/0/1
    R2(config-if)#ip ospf hello-interval 30
    R2(config-if)#ip ospf dead-interval 120
    R2(config-if)#ex
    R2(config)#interface loopback 1
    R2(config-if)#ip ospf network point-to-point 
    R2(config-if)#ex
    R2(config)#router ospf 56
    R2(config-router)#passive-interface loopback 1
    R2(config-router)#auto-cost reference-bandwidth 1000
    R2(config-router)#ex
##### Шаг 2. Убедитесь, что оптимизация OSPFv2 реализовалась.
###### Проверка R1
    show ip ospf neighbor 
    Neighbor ID     Pri   State           Dead Time   Address         Interface
    2.2.2.2           1   FULL/BDR        00:01:56    10.53.0.2       GigabitEthernet0/0/1
    R1#show ip route ospf 
    O    192.168.1.0 [110/10] via 10.53.0.2, 00:01:52, GigabitEthernet0/0/1
    R1#show ip ospf interface g0/0/1
    GigabitEthernet0/0/1 is up, line protocol is up
      Internet address is 10.53.0.1/24, Area 0
      Process ID 56, Router ID 1.1.1.1, Network Type BROADCAST, Cost: 10
      Transmit Delay is 1 sec, State DR, Priority 50
      Designated Router (ID) 1.1.1.1, Interface address 10.53.0.1
      Backup Designated Router (ID) 2.2.2.2, Interface address 10.53.0.2
      Timer intervals configured, Hello 30, Dead 120, Wait 120, Retransmit 5
        Hello due in 00:00:05
      Index 1/1, flood queue length 0
      Next 0x0(0)/0x0(0)
      Last flood scan length is 1, maximum is 1
      Last flood scan time is 0 msec, maximum is 0 msec
      Neighbor Count is 1, Adjacent neighbor count is 1
        Adjacent with neighbor 2.2.2.2  (Backup Designated Router)
      Suppress hello for 0 neighbor(s)
###### Проверка R2
    R2#show ip ospf interface g0/0/1
    GigabitEthernet0/0/1 is up, line protocol is up
      Internet address is 10.53.0.2/24, Area 0
      Process ID 56, Router ID 2.2.2.2, Network Type BROADCAST, Cost: 10
      Transmit Delay is 1 sec, State BDR, Priority 1
      Designated Router (ID) 1.1.1.1, Interface address 10.53.0.1
      Backup Designated Router (ID) 2.2.2.2, Interface address 10.53.0.2
      Timer intervals configured, Hello 30, Dead 120, Wait 120, Retransmit 5
        Hello due in 00:00:22
      Index 1/1, flood queue length 0
      Next 0x0(0)/0x0(0)
      Last flood scan length is 1, maximum is 1
      Last flood scan time is 0 msec, maximum is 0 msec
      Neighbor Count is 1, Adjacent neighbor count is 1
        Adjacent with neighbor 1.1.1.1  (Designated Router)
      Suppress hello for 0 neighbor(s)
