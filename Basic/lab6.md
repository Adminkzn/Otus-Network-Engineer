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
    R1(config)#clock timezone MSK 3
    R1(config)#exit
    R1#clock set 10:00:00 1 oct 2025
    


