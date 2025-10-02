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
    
