### Лабораторная работа. Базовая настройка коммутатора

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/107e05e07fadad109b5df13bd89fd537c581f3ab/img/lab%201-1.jpg?raw=true)


#### Задачи
##### Часть 1. Проверка конфигурации коммутатора по умолчанию
##### Часть 2. Создание сети и настройка основных параметров устройстваЧасть 2. Создание сети и настройка основных параметров устройства
•	Настройте базовые параметры коммутатора.
•	Настройте IP-адрес для ПК.
##### Часть 3. Проверка сетевых подключенийЧасть 3. Проверка сетевых подключений
•	Отобразите конфигурацию устройства.
•	Протестируйте сквозное соединение, отправив эхо-запрос.
•	Протестируйте возможности удаленного управления с помощью Telnet.

#### Часть 1. Создание сети и проверка настроек коммутатора по умолчанию
##### Шаг 1. Создайте сеть согласно топологии.
Почему нужно использовать консольное подключение для первоначальной настройки коммутатора? Почему нельзя подключиться к коммутатору через Telnet или SSH?
По умолчанию Telnet или SSH выключены.

#### Шаг 2. Проверьте настройки коммутатора по умолчанию.
##### Общие сведения/сценарий
**а.** С помощью команды enable зашел в приыелигированый режим и выполнил команду show running-config. Убедился, что конфигурыция коммутатора пустая.

**b.** Коммутатор 2960 имеет 24 FastEthernet интерфейсов и 2 Gigabit Ethernet  интерфейса, диопозон значений vty линий 0-4 и 5-15.

**с.** startup configuration еще нет.

**d.** 
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-2.jpg?raw=true)

Интерфейс VLAN выключен, ip адресс не назначен 

MAC-адресс 0002.4aaa.44ae ???

**e.** Интерфейс VLAN выключен

**f.**  Интерфейс VLAN выключен

**g.** 
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-3.jpg?raw=true)

Коммутатор работает под Version 15.0(2)SE4

Файл образа системы C2960-LANBASEK9-M

**h** 
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-4.jpg?raw=true)

интерфейс включен, MAC-адресс 0060.5c0a.1006, Full-duplex, 100Mb/s

**i.** 2960-lanbasek9-mz.150-2.SE4.bin

#### Часть 2. Настройка базовых параметров сетевых устройств
##### Шаг 1. Настройте базовые параметры коммутатора.

**a.**
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-5.jpg?raw=true)

**b**
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-6.jpg?raw=true)

**c.** 
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-7.jpg?raw=true)

**d.**
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-8.jpg?raw=true)

#### Шаг 2. Настройте IP-адрес на компьютере PC-A.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-9.jpg?raw=true)

#### Часть 3. Проверка сетевых подключений
##### Шаг 1. Отобразите конфигурацию коммутатора.
Current configuration : 1316 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname S1
!
enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
!
!
!
no ip domain-lookup
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
!
banner motd ^CUnauthorized access is strictly prohibited. ^C
!
!
!
line con 0
 password 7 0822455D0A16
 logging synchronous
 login
!
line vty 0 4
 password 7 0822455D0A16
 login
 transport input telnet
line vty 5 15
 login
!
!
!
!
end

##### Шаг 2. Протестируйте сквозное соединение, отправив эхо-запрос.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-10.jpg?raw=true)

##### Шаг 3. Проверьте удаленное управление коммутатором S1.
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%201-11.jpg?raw=true)

#### Вопросы для повторения
**1.**Виртуальные порты для удаленого подключения и управления устройством по telnet и ssh
**2.** использовать ssh


