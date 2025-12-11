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

####Часть 2. Настройка сетей VLAN на коммутаторах.
##### Шаг 1. Создайте сети VLAN на коммутаторах.
##### Шаг 2. Назначьте сети VLAN соответствующим интерфейсам коммутатора.
###### Настройка на примере S2
    S2(config)#vlan 20
    S2(config-vlan)#name Management
    S2(config-vlan)#ex
    S2(config)#vlan 30
    S2(config-vlan)#name Operations
    S2(config-vlan)#ex
    S2(config)#vlan 40
    S2(config-vlan)#name Sales
    S2(config-vlan)#ex
    S2(config)#vlan 999
    S2(config-vlan)# name ParkingLot
    S2(config-vlan)#ex
    S2(config)#vlan 1000
    S2(config-vlan)#name Native
    S2(config-vlan)#ex
    S2(config)#interface vlan 20
    S2(config-if)#ip address 10.20.0.3 255.255.255.0
    S2(config-if)#no shutdown 
    S2(config-if)#ex
    S2(config)#ip default-gateway 10.20.0.1
    S2(config)#interface range fastEthernet 0/2-4
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
	S2(config-if-range)#shutdown
	S2(config-if-range)#ex
    S2(config)#interface range fastEthernet 0/6-17
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
	S2(config-if-range)#shutdown
    S2(config-if-range)#ex
    S2(config)#interface range fastEthernet 0/19-24
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
	S2(config-if-range)#shutdown
    S2(config-if-range)#ex
    S2(config)#interface range gigabitEthernet 0/1-2
    S2(config-if-range)#switchport mode access 
    S2(config-if-range)#switchport access vlan 999
	S2(config-if-range)#shutdown
    S2(config-if-range)#ex
    
#### Часть 3. ·Настройте транки (магистральные каналы).
##### Шаг 1. Вручную настройте магистральный интерфейс F0/1.
##### Шаг 2. Вручную настройте магистральный интерфейс F0/5 на коммутаторе S1.
###### Настройка на примере S2
    S2(config)#interface fastEthernet 0/18
    S2(config-if)#switchport mode access 
    S2(config-if)#switchport access vlan 40
    S2(config-if)#no shutdown 
    S2(config-if)#ex
    S2(config)#interface fastEthernet 0/5
    S2(config-if)#switchport mode access 
    S2(config-if)#switchport access vlan 20
    S2(config-if)#no shutdown 
    S2(config-if)#ex
    S2(config)#interface fastEthernet 0/1
    S2(config-if)#switchport mode trunk 
    S2(config-if)#switchport trunk native vlan 1000
    S2(config-if)#switchport trunk allowed vlan 20,40,1000
    S2(config-if)#no shutdown 
    S2(config-if)#ex

#### Часть 4. Настройте маршрутизацию.
##### Шаг 1. Настройка маршрутизации между сетями VLAN на R1.
##### Шаг 2. Настройка интерфейса R2 g0/0/1 с использованием адреса из таблицы и маршрута по умолчанию с адресом следующего перехода 10.20.0.1

#### Часть 5. Настройте удаленный доступ
##### Шаг 1. Настройте все сетевые устройства для базовой поддержки SSH.
###### Настройка на примере S2
    S1(config)#username SSHadmin privilege 15 secret $cisco123!
    S1(config)#ip domain-name ccna-lab.com
    S1(config)#crypto key generate rsa general-keys modulus 1024
    S1(config)#line vty 0 4
    S1(config-line)# transport input ssh
    S1(config-line)# login local
    S1(config-line)# exit
    S1(config)#
##### Шаг 2. Включите защищенные веб-службы с проверкой подлинности на R1.

#### Часть 6. Проверка подключения

#### Часть 7. Настройка и проверка списков контроля доступа (ACL)
