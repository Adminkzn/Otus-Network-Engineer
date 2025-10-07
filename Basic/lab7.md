![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%207-1.jpg?raw=true)
#### Часть 1:	Создание сети и настройка основных параметров устройства
##### Шаг 1:	Создайте сеть согласно топологии.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%207-2.jpg?raw=true)
##### Шаг 2:	Выполните инициализацию и перезагрузку коммутаторов.
Выполнено
##### Шаг 3:	Настройте базовые параметры каждого коммутатора.
    Switch>enable 
    Switch#conf t
    Switch(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#hostname S1
    S1(config)#service password-encryption 
    S1(config)#enable secret cisco
    S1(config)#banner motd #!!!ACCESS DENIED!!!#
    S1(config)#line console 0
    S1(config-line)#logging synchronous 
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#exec-timeout 10 0
    S1(config-line)#exit
    S1(config)#interface vlan 1
    S1(config-if)#ip address 192.168.1.1 255.255.255.0
    S1(config-if)#no shutdown 
    S1(config-if)#exit
    S1(config)#ip domain-name company.local
    S1(config)#crypto key generate rsa
    How many bits in the modulus [512]: 2048
    S1(config)#ip ssh version 2
    S1(config)#username admin privilege 15 secret cisco
    S1(config)#line vty 0 15
    S1(config-line)#login local 
    S1(config-line)#transport input ssh 
    S1(config-line)#exec-timeout 10 0
    S1(config-line)#exit
    S1(config)#exit
    S1#copy running-config startup-config 
	

#### Часть 2:	Определение корневого моста
##### Шаг 1:	Отключите все порты на коммутаторах.
    S1(config)#interface range fa0/1-24
    S1(config-if-range)#shutdown
    S1(config-if-range)#exit
    
    S2(config)#interface range fa0/1-24  
    S2(config-if-range)#shutdown
    S2(config-if-range)#exit
    
    S3(config)#interface range fa0/1-24
    S3(config-if-range)#shutdown
    S3(config-if-range)#exit
##### Шаг 2:	Настройте подключенные порты в качестве транковых. 
##### Шаг 3:	Включите порты F0/2 и F0/4 на всех коммутаторах.
    S1(config)#interface range fa0/2, fa0/4
    S1(config-if-range)#switchport mode trunk
    S1(config-if-range)#no shutdown
    S1(config-if-range)#exit
    
    S2(config)#interface range fa0/2, fa0/4
    S2(config-if-range)#switchport mode trunk
    S2(config-if-range)#no shutdown
    S2(config-if-range)#exit
    
    S3(config)#interface range fa0/2, fa0/4
    S3(config-if-range)#switchport mode trunk
    S3(config-if-range)#no shutdown
    S3(config-if-range)#exit
##### Шаг 4:	Отобразите данные протокола spanning-tree.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%207-7.jpg?raw=true)

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%207-8.jpg?raw=true)

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%207-9.jpg?raw=true)
