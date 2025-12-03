![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2014-1.jpg?raw=true)

#### Часть 1. Создание сети и настройка основных параметров устройства
##### Шаг 1. Подключите кабели сети согласно приведенной топологии.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2014-2.jpg?raw=true)

##### Шаг 2. Произведите базовую настройку маршрутизаторов.
###### R1
    Router>en
    Router#conf t
    Router(config)#hostname R1
    R1(config)#no ip domain-lookup 
    R1(config)#enable secret class
    R1(config)#line console 0
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#exit
    R1(config)#line vty 0 4
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#exit
    R1(config)#service password-encryption 
    R1(config)#banner motd #R1#
    R1(config)#interface gigabitEthernet 0/0/0
    R1(config-if)#ip address 209.165.200.230 255.255.255.248
    R1(config-if)#no shutdown 
    R1(config-if)#ex
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#ip ad
    R1(config-if)#ip address 192.168.1.1 255.255.255.0
    R1(config-if)#no sh
    R1(config-if)#no shutdown 
    R1(config-if)#ex
    R1(config)#ip route 0.0.0.0 0.0.0.0 209.165.200.225
    R1(config)#ex
    R1#write memory 
	

##### Шаг 3. Настройте базовые параметры каждого коммутатора.
###### S1

    Switch>enable 
    Switch#conf t
    Switch(config)#hostname S1
    S1(config)#no ip domain-l
    S1(config)#banner motd #S1#
    S1(config)#service password-encryption 
    S1(config)#enable secret class
    S1(config)#interface vlan 1
    S1(config-if)#ip address 192.168.1.11 255.255.255.0
    S1(config-if)#no shutdown 
    S1(config-if)#ex
    S1(config)#interface range fastEthernet 0/2-4
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex
    S1(config)#interface range fastEthernet 0/7-24
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex
    S1(config)#interface range gigabitEthernet 0/1-2
    S1(config-if-range)#shutdown 
    S1(config)#exit 
    S1#write memory 

#### Часть 2. Настройка и проверка NAT для IPv4.
##### Шаг 1. Настройте NAT на R1, используя пул из трех адресов 209.165.200.226-209.165.200.228. 
##### Шаг 2. Проверьте и проверьте конфигурацию. 
