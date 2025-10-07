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

###### 1. Какой коммутатор является корневым мостом?
S2 (потому что в выводе S2 указано "This bridge is the root")

###### 2. Почему этот коммутатор был выбран протоколом spanning-tree в качестве корневого моста?
Потому что у него наименьший MAC-адрес (0001.C72C.AC88) при одинаковых приоритетах (32769). Все коммутаторы имеют одинаковый приоритет 32769, поэтому выбор пал на коммутатор с наименьшим MAC-адресом.

###### 3. Какие порты на коммутаторе являются корневыми портами?
S1: F0/2 (Root FWD)
S3: F0/2 (Root FWD)

###### 4. Какие порты на коммутаторе являются назначенными портами?
S1: F0/4 (Desg FWD)
S2: F0/2, F0/4 (Desg FWD)
S3: нет назначенных портов

###### 5. Какой порт отображается в качестве альтернативного и в настоящее время заблокирован?
S3 F0/4 (Altn BLK)

###### 6. Почему протокол spanning-tree выбрал этот порт в качестве невыделенного (заблокированного) порта?
STP блокирует порт F0/4 на S3 для предотвращения петель в сети. Оба пути от S3 к корневому мосту S2 имеют одинаковую стоимость (19), но порт F0/2 был выбран как корневой порт потому что номер порта F0/2 (2) меньше номера порта F0/4 (4).

#### Часть 3:	Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов
##### Шаг 1:	Определите коммутатор с заблокированным портом.
S3 F0/4 (Altn BLK)
##### Шаг 2:	Измените стоимость порта.
S1(config)# interface f0/2
S1(config-if)# spanning-tree vlan 1 cost 18
##### Шаг 3:	Просмотрите изменения протокола spanning-tree.
Изменение стоимости на S1 не повлияло на выбор порта на S3, потому что S3 по-прежнему видит более короткий путь напрямую к корневому мосту через свой порт F0/2.

#### Часть 4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов
##### a.	Включите порты F0/1 и F0/3 на всех коммутаторах.



