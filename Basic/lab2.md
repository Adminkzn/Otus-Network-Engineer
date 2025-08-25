![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-1.jpg?raw=true)

#### Часть 1. Создание и настройка сети

##### Шаг 1. Подключите сеть в соответствии с топологией.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-2.jpg?raw=true)

##### Шаг 2. Настройте узлы ПК.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-3.jpg?raw=true)

##### Шаг 3. Выполните инициализацию и перезагрузку коммутаторов.
Выполнил

##### Шаг 4. Настройте базовые параметры каждого коммутатора.
##### S1
    Switch(config)#no ip domain-lookup
    Switch(config)#hostname S1
    S1(config)#service password-encryption
    S1(config)#enable secret class
    S1(config)#banner motd #SW1#
    S1(config)#interface vlan 1
    S1(config-if)#ip address 192.168.1.11 255.255.255.0
    S1(config-if)#no shutdown
    S1(config-if)#exit
    S1(config)#line console 0
    S1(config-line)#logging synchronous
    S1(config-line)#password cisco
    S1(config-line)#login

##### S2
    Switch(config)#no ip domain-lookup
    Switch(config)#hostname S2
    S1(config)#service password-encryption
    S1(config)#enable secret class
    S1(config)#banner motd #SW2#
    S1(config)#interface vlan 1
    S1(config-if)#ip address 192.168.1.12 255.255.255.0
    S1(config-if)#no shutdown
    S1(config-if)#exit
    S1(config)#line console 0
    S1(config-line)#logging synchronous
    S1(config-line)#password cisco
    S1(config-line)#login

#### Часть 2. Изучение таблицы МАС-адресов коммутатора
##### Шаг 1. Запишите МАС-адреса сетевых устройств.

PC-A  0007.EC85.66B2
PC-B  0002.173E.B29A

S1 00d0.97e4.5a92
S2 000c.cf84.a601

##### S1
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-4.jpg?raw=true)

##### S2
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-5.jpg?raw=true)

В мак таблицах коммутаторов содержатся адреса друг друга.

В рамках одного VLAN коммутатор в нормальном состоянии ассоциирует один уникальный MAC-адрес устройства только с одним портом в своей таблице коммутации. В нашем случае можно определить по номеру порта. 

#### Шаг 3. Очистите таблицу МАС-адресов коммутатора S2 и снова отобразите таблицу МАС-адресов.

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-6.jpg?raw=true)

#### Шаг 4. С компьютера PC-B отправьте эхо-запросы устройствам в сети и просмотрите таблицу МАС-адресов коммутатора.

**a.**  В  таблице пусто


**b.**

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-7.jpg?raw=true)


**c.**

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%202-8.jpg?raw=true)

    0001.972b.5101 - fastEthernet 0/1 на S1
    0002.173E.B29A - PC-B 
    0007.EC85.66B2 - PC-A 
    00d0.97e4.5a92 - S1 

#### Вопрос для повторения
1. Перегрузка широковещательным трафиком, заполнение полосы пропускания, нагрузка на CPU SW. Время жизни адресов в мак таблицах ограничено и хостам приходится постоянно обновлять с вою таблицу, снова помсылая Arp запросы.
2. Переполнение таблиц MAC-адресов на коммутаторах.
3. Проблемы безопасности. Протокол Arp работает на доверии. Атака "человек посередине".










