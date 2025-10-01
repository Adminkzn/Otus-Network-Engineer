### Лабораторная работа - Внедрение маршрутизации между виртуальными локальными сетями
#### ТопологияТопология
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-1.jpg?raw=true)
#### Таблица адресации
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-2.jpg?raw=true)
#### Таблица VLAN
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-3.jpg?raw=true)

#### Задачи
Часть 1. Создание сети и настройка основных параметров устройства

Часть 2. Создание сетей VLAN и назначение портов коммутатора

Часть 3. Настройка транка 802.1Q между коммутаторами.

Часть 4. Настройка маршрутизации между сетями VLAN

Часть 5. Проверка, что маршрутизация между VLAN работает

#### Часть 1. Создание сети и настройка основных параметров устройства
##### Шаг 1. Создайте сеть согласно топологии.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-4.jpg?raw=true)
##### Шаг 2. Настройте базовые параметры для маршрутизатора.
    
    Router>enable 
    Router#configure terminal 
    Router(config)#hostname R1
    R1(config)#no ip domain-lookup 
    R1(config)#enable secret class
    R1(config)#line console 0
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#logging synchronous 
    R1(config-line)#exec-timeout 5 0
    R1(config-line)#exit 
    R1(config)#line vty 0 4
    R1(config-line)#password cisco
    R1(config-line)#login
    R1(config-line)#exit 
    R1(config)#service password-encryption 
    R1(config)#banner motd #Access denied#
    R1(config)#exit 
    R1#copy running-config startup-config 
    R1#conf t
    R1#conf terminal 
    R1(config)#clock timezone MSK 3
    R1(config)#exit
    R1#clock set 10:00:00 1 oct 2025
    
##### Шаг 3. Настройте базовые параметры каждого коммутатора.
    Switch>enable 
    Switch#configure terminal 
    Switch(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#enable secret class
    S1(config)#line console 0
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#logging synchronous 
    S1(config-line)#exec-timeout 5 0
    S1(config-line)#exit 
    S1(config)#line vty 0 15 
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#logging synchronous 
    S1(config-line)#exit 
    S1(config)#service password-encryption 
    S1(config)#banner motd #access denied#
    S1(config)#clock timezone MSK 3
    S1(config)#exit
    S1#clock set 10:29:00 1 october 2025
	S1#copy running-config startup-config 
	
##### Шаг 4. Настройте узлы ПК.
###### PC-A
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-5.jpg?raw=true)
###### PC-B
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-6.jpg?raw=true)
#### Часть 2. Создание сетей VLAN и назначение портов коммутатора
##### Шаг 1. Создайте сети VLAN на коммутаторах.
###### S1
    S1#conf t
    S1(config)#vlan 10
    S1(config-vlan)#name Management
    S1(config-vlan)#exit
    S1(config)#vlan 20
    S1(config-vlan)#name Sales
    S1(config-vlan)#exit
    S1(config)#vlan 30
    S1(config-vlan)#name Operations
    S1(config-vlan)#exit
    S1(config)#vlan 999
    S1(config-vlan)#name Parking_Lot
    S1(config-vlan)#exit 
    S1(config)#vlan 1000
    S1(config-vlan)#name Native
    S1(config-vlan)#exit 
	S1(config)#interface vlan 10    
    S1(config-if)#ip address 192.168.10.11 255.255.255.0
    S1(config)#ip default-gateway 192.168.10.1
	
    S1(config)#interface range fastEthernet 0/2-4, fastEthernet 0/7-24, gigabitEthernet 0/1-2
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#exit 
###### S2
	S2#conf t
    S2(config)#interface range fastEthernet 0/2-17, fastEthernet 0/19-24, gigabitEthernet 0/1-2
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
    S2(config-if-range)#shutdown 
##### Шаг 2. Назначьте сети VLAN соответствующим интерфейсам коммутатора.
###### S1
    S1conf t
    S1(config)#interface fastEthernet 0/6
    S1(config-if)#switchport mode access 
    S1(config-if)#switchport access vlan 20
    S1(config-if)#no shutdown 
    S1(config-if)#exit

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-8.jpg?raw=true)
###### S2
    S2(config)#interface fastEthernet 0/18
    S2(config-if)#switchport mode access 
    S2(config-if)#switchport access vlan 30
	S1(config-if)#no shutdown
    S2(config-if)#exit

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-9.jpg?raw=true)

### Лабораторная работа - Внедрение маршрутизации между виртуальными локальными сетями
#### ТопологияТопология
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-1.jpg?raw=true)
#### Таблица адресации
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-2.jpg?raw=true)
#### Таблица VLAN
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-3.jpg?raw=true)

#### Задачи
Часть 1. Создание сети и настройка основных параметров устройства

Часть 2. Создание сетей VLAN и назначение портов коммутатора

Часть 3. Настройка транка 802.1Q между коммутаторами.

Часть 4. Настройка маршрутизации между сетями VLAN

Часть 5. Проверка, что маршрутизация между VLAN работает

#### Часть 1. Создание сети и настройка основных параметров устройства
##### Шаг 1. Создайте сеть согласно топологии.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-4.jpg?raw=true)
##### Шаг 2. Настройте базовые параметры для маршрутизатора.
    
    Router>enable 
    Router#configure terminal 
    Router(config)#hostname R1
    R1(config)#no ip domain-lookup 
    R1(config)#enable secret class
    R1(config)#line console 0
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#logging synchronous 
    R1(config-line)#exec-timeout 5 0
    R1(config-line)#exit 
    R1(config)#line vty 0 4
    R1(config-line)#password cisco
    R1(config-line)#login
    R1(config-line)#exit 
    R1(config)#service password-encryption 
    R1(config)#banner motd #Access denied#
    R1(config)#exit 
    R1#copy running-config startup-config 
    R1#conf t
    R1#conf terminal 
    R1(config)#clock timezone MSK 3
    R1(config)#exit
    R1#clock set 10:00:00 1 oct 2025
    
##### Шаг 3. Настройте базовые параметры каждого коммутатора.
    Switch>enable 
    Switch#configure terminal 
    Switch(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#enable secret class
    S1(config)#line console 0
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#logging synchronous 
    S1(config-line)#exec-timeout 5 0
    S1(config-line)#exit 
    S1(config)#line vty 0 15 
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#logging synchronous 
    S1(config-line)#exit 
    S1(config)#service password-encryption 
    S1(config)#banner motd #access denied#
    S1(config)#clock timezone MSK 3
    S1(config)#exit
    S1#clock set 10:29:00 1 october 2025
	S1#copy running-config startup-config 
	
##### Шаг 4. Настройте узлы ПК.
###### PC-A
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-5.jpg?raw=true)
###### PC-B
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-6.jpg?raw=true)
#### Часть 2. Создание сетей VLAN и назначение портов коммутатора
##### Шаг 1. Создайте сети VLAN на коммутаторах.
###### S1
    S1#conf t
    S1(config)#vlan 10
    S1(config-vlan)#name Management
    S1(config-vlan)#exit
    S1(config)#vlan 20
    S1(config-vlan)#name Sales
    S1(config-vlan)#exit
    S1(config)#vlan 30
    S1(config-vlan)#name Operations
    S1(config-vlan)#exit
    S1(config)#vlan 999
    S1(config-vlan)#name Parking_Lot
    S1(config-vlan)#exit 
    S1(config)#vlan 1000
    S1(config-vlan)#name Native
    S1(config-vlan)#exit 
	S1(config)#interface vlan 10    
    S1(config-if)#ip address 192.168.10.11 255.255.255.0
    S1(config)#ip default-gateway 192.168.10.1
	
    S1(config)#interface range fastEthernet 0/2-4, fastEthernet 0/7-24, gigabitEthernet 0/1-2
    S1(config-if-range)#switchport mode access 
    S1(config-if-range)#switchport access vlan 999
    S1(config-if-range)#shutdown 
    S1(config-if-range)#exit 
###### S2
	S2#conf t
    S2(config)#interface range fastEthernet 0/2-17, fastEthernet 0/19-24, gigabitEthernet 0/1-2
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
    S2(config-if-range)#shutdown 
##### Шаг 2. Назначьте сети VLAN соответствующим интерфейсам коммутатора.
###### S1
    S1conf t
    S1(config)#interface fastEthernet 0/6
    S1(config-if)#switchport mode access 
    S1(config-if)#switchport access vlan 20
    S1(config-if)#no shutdown 
    S1(config-if)#exit

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-8.jpg?raw=true)
###### S2
    S2(config)#interface fastEthernet 0/18
    S2(config-if)#switchport mode access 
    S2(config-if)#switchport access vlan 30
	S1(config-if)#no shutdown
    S2(config-if)#exit
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-9.jpg?raw=true)

#### Часть 3. Конфигурация магистрального канала стандарта 802.1Q между коммутаторами
##### Шаг 1. Вручную настройте магистральный интерфейс F0/1 на коммутаторах S1 и S2.
    S1#conf t
    S1(config)#interface f 0/1
    S1(config-if)#switchport mode trunk 
    S1(config-if)#switchport trunk native vlan 1000
    S1(config-if)#switchport trunk allowed vlan 10,20,30,1000
    S1(config-if)#no shutdown 
    S1(config-if)#exit
##### Шаг 2. Вручную настройте магистральный интерфейс F0/5 на коммутаторе S1.
    S1(config)#interface f0/5
    S1(config-if)#switchport mode trunk 
    S1(config-if)#switchport trunk native vlan 1000
    S1(config-if)#switchport trunk allowed vlan 10,20,30,1000
    S1(config-if)#no shutdown 
#### Часть 4. Настройка маршрутизации между сетями VLAN
    R1#conf t
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#no shutdown 
    R1(config-if)#interface gigabitEthernet 0/0/1.10
    R1(config-subif)#encapsulation dot1Q 10
    R1(config-subif)#ip address 192.168.10.1 255.255.255.0
    R1(config-subif)#no shutdown 
    R1(config-subif)#exit 
    R1(config)#interface gigabitEthernet 0/0/1.20
    R1(config-subif)#encapsulation dot1Q 20
    R1(config-subif)#ip address 192.168.20.1 255.255.255.0
    R1(config-subif)#no shutdown 
    R1(config-subif)#exit
    R1(config)#interface gigabitEthernet 0/0/1.30
    R1(config-subif)#encapsulation dot1Q 30
    R1(config-subif)#ip address 192.168.30.1 255.255.255.0
    R1(config-subif)#no shutdown 
    R1(config-subif)#exit 
    R1(config)#interface gigabitEthernet 0/0/1.1000
    R1(config-subif)#encapsulation dot1Q 1000 native 
    R1(config-subif)#no shutdown 
    R1(config-subif)#no ip address 
    R1(config-subif)#exit
    R1(config)#ip routing 
	
#### Часть 5. Проверьте, работает ли маршрутизация между VLAN
##### Шаг 1. Выполните следующие тесты с PC-A. Все должно быть успешно.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-10.jpg?raw=true)
##### Шаг 2. Пройдите следующий тест с PC-B
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%206-11.jpg?raw=true)

#### Что произойдет, если G0/0/1 на R1 будет отключен?
Перестанет работать межвлановая маршрутизация
