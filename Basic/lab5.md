### Лабораторная работа. Доступ к сетевым устройствам по протоколу SSH
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-1.jpg?raw=true)
#### Часть 1. Настройка основных параметров устройств и топологии сети


##### Cеть согласно топологии
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-4.jpg?raw=true)

##### Базовая настройка S1
    Switch>enable 
    Switch#conf t
    Switch(config)#no ip domain-lookup 
    Switch(config)#hostname S1
    S1(config)#service password-encryption 
    S1(config)#enable secret cisco
    S1(config)#banner motd #!!! UNAUTHORIZED ACCESS PROHIBITED !!!#
    S1(config)#line console 0
    S1(config-line)#logging synchronous 
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#exec-timeout 5 0
    S1(config-line)#exit
    S1(config)#interface vlan 1
    S1(config-if)#ip address 192.168.1.11 255.255.255.0
    S1(config-if)#no shutdown 
    S1(config-if)#exit
    S1(config)#ip default-gateway 192.168.1.1
    S1(config)#exit 
    S1#copy running-config startup-config 

##### Базовая настройка R1
    Router>enable 
    Router#conf t
    Router(config)#no ip domain-lookup 
    Router(config)#hostname R1
    R1(config)#enable secret cisco
    R1(config)#banner motd #!!! UNAUTHORIZED ACCESS PROHIBITED !!!#
    R1(config)#line console 0
    R1(config-line)#logging synchronous 
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#exec-timeout 5 0
    R1(config-line)#exit 
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#ip address 192.168.1.1 255.255.255.0
    R1(config-if)#no shutdown 
    R1(config-if)#exit 
    R1#copy running-config startup-config 

##### Настройка PC-A
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-2.jpg?raw=true)

##### Проверьте подключение к сети.
Команда ping c PC-A до R1
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-3.jpg?raw=true)

#### Часть 2. Настройка маршрутизатора для доступа по протоколу SSH
##### Настройка R1
    R1(config)#ip domain-name company.local
    R1(config)#crypto key generate rsa general-keys modulus 2048
    The name for the keys will be: R1.company.local
    
    % The key modulus size is 2048 bits
    % Generating 2048 bit RSA keys, keys will be non-exportable...[OK]
    *Mar 1 1:40:54.482: %SSH-5-ENABLED: SSH 1.99 has been enabled
    R1(config)#exit 
    R1#conf t
    R1#conf terminal 
    R1(config)#username admin privilege 15 secret Adm1nP@55
    R1(config)#ip ssh version 2
    R1(config)#line vty 0 4
    R1(config-line)#login local 
    R1(config-line)#transport input ssh
    R1(config-line)#exit 
    R1(config)#exit 
    R1#copy running-config startup-config
	
##### Установите соединение с маршрутизатором по протоколу SSH c PC-A
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-5.jpg?raw=true)


#### Часть 3. Настройка коммутатора для доступа по протоколу SSH
##### Настройка S1
    S1(config)#ip domain-name company.local
    S1(config)#crypto key generate rsa
    The name for the keys will be: S1.company.local
    Choose the size of the key modulus in the range of 360 to 2048 for your
      General Purpose Keys. Choosing a key modulus greater than 512 may take
      a few minutes.
    
    How many bits in the modulus [512]: 2048
    % Generating 2048 bit RSA keys, keys will be non-exportable...[OK]
    
    S1(config)#ss
    *Mar 1 2:15:59.940: %SSH-5-ENABLED: SSH 1.99 has been enabled
    S1(config)#ip ssh version 2
    S1(config)#username admin privilege 15 secret Adm1nP@55
    S1(config)#line vty 0 4
    S1(config-line)#login local 
    S1(config-line)#transport input ssh 
    S1(config-line)#exit 
    S1(config)#exit 
    S1#copy running-config startup-config 
##### Установите соединение с коммутатором по протоколу SSH c PC-A
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-6.jpg?raw=true)

### Часть 4. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%205-7.jpg?raw=true)

### Вопрос для повторения
Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователя?
Нужно настроить локальную базу пользователей

