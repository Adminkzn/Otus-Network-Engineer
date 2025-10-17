![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%208-1.jpg?raw=true)
### Часть 1.	Создание сети и настройка основных параметров устройства

#### Шаг 1.	Создание схемы адресации

**a. Подсеть A:**

Сеть: 192.168.1.0/26

G0/0/1.100: 192.168.1.1

**b. Подсеть B:**

Сеть: 192.168.1.64/27

R1 G0/0/1.200: 192.168.1.65

S1 VLAN 200: 192.168.1.66

**c. Подсеть C:**

Сеть: 192.168.1.96/28

R2 G0/0/1: 192.168.1.97

#### Шаг 2.	Создайте сеть согласно топологии
![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%208-2.jpg?raw=true)
#### Шаг 3.	Произведите базовую настройку маршрутизаторов
Настройка для R1 и R2 одинакова 

    Router>
    Router>enable 
    Router#conf terminal 
    Enter configuration commands, one per line.  End with CNTL/Z.
    Router(config)#hostname R1
    R1(config)#no ip domain-lookup 
    R1(config)#service password-encryption 
    R1(config)#enable secret class
    R1(config)#banner motd #!!!ACCESS DENIED!!!#
    R1(config)#line console 0
    R1(config-line)#logging synchronous 
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#exec-timeout 10 0
    R1(config-line)#exit
    R1(config)#line vty 0 4
    R1(config-line)#logging synchronous 
    R1(config-line)#password cisco
    R1(config-line)#login 
    R1(config-line)#exec-timeout 10 0
    R1(config-line)#exit
    R1(config)#exit
    R1#clock set 6:52:00 17 november 2025 
    R1#copy running-config startup-config
    %SYS-5-CONFIG_I: Configured from console by console
    R1#copy running-config startup-config
    Destination filename [startup-config]? 
    Building configuration...
    [OK]
    R1#

#### Шаг 4.	Настройка маршрутизации между сетями VLAN на маршрутизаторе R1
    R1(config)#
    R1(config)#interface GigabitEthernet 0/0/1
    R1(config-if)#no shutdown
    R1(config-subif)#exit
    R1(config)#
    R1(config)#interface GigabitEthernet 0/0/1.1000
    R1(config-subif)#encapsulation dot1Q 1000 native 
    R1(config-subif)#description Vlan 1000 native
    R1(config-subif)#exit
    R1(config)#
    R1(config)#interface GigabitEthernet 0/0/1.100
    R1(config-subif)#encapsulation dot1Q 100
    R1(config-subif)#ip address 192.168.1.1 255.255.255.192
    R1(config-subif)#description Vlan 100 Client
    R1(config-subif)#no shutdown 
    R1(config-subif)#exit
    R1(config)#
    R1(config)#interface GigabitEthernet 0/0/1.200
    R1(config-subif)#encapsulation dot1Q 200
    R1(config-subif)#description Vlan 200 Management
    R1(config-subif)#ip address 192.168.1.65 255.255.255.224
    R1(config-subif)#no shutdown 
    R1(config-subif)#exit
    R1(config)#
	R1#show ip interface brief 
    Interface              IP-Address      OK? Method Status                Protocol 
    GigabitEthernet0/0/0   unassigned      YES unset  administratively down down 
    GigabitEthernet0/0/1   unassigned      YES unset  up                    up 
    GigabitEthernet0/0/1.100192.168.1.1     YES manual up                    up 
    GigabitEthernet0/0/1.200192.168.1.65    YES manual up                    up 
    GigabitEthernet0/0/1.1000unassigned      YES unset  up                    up 
    GigabitEthernet0/0/2   unassigned      YES unset  administratively down down 
    Vlan1                  unassigned      YES unset  administratively down down
    R1#
    R1#ping 192.168.1.1

    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 192.168.1.1, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 0/1/4 ms

    R1#ping 192.168.1.65

    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 192.168.1.65, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 1/3/8 ms

#### Шаг 5.	Настройте G0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов
**a.	Настройте G0/0/1 на R2**
    R2(config)#interface gigabitEthernet 0/0/1
    R2(config-if)#ip address 192.168.1.97 255.255.255.240
    R2(config-if)#no shutdown

**b.	Настройте интерфейс G0/0/0**
    
    R1(config)#interface gigabitEthernet 0/0/0
    R1(config-if)#ip address 10.0.0.1 255.255.255.252
    R1(config-if)#no shutdown 
    R1(config-if)#exit
    R1(config)#ip route 0.0.0.0 10.0.0.2
	
    R2(config)#interface g0/0/0
    R2(config-if)#ip address 10.0.0.2 255.255.255.252
    R2(config-if)#no shutdown 
    R2(config-if)#exit
    R2(config)#ip route 0.0.0.0 10.0.0.1
    
    
#### Шаг 6.	Настройте базовые параметры каждого коммутатора
#### Шаг 7.	Создайте сети VLAN на коммутаторе S1
#### Шаг 8.	Назначьте сети VLAN соответствующим интерфейсам коммутатора
#### Шаг 9.	Вручную настройте интерфейс S1 F0/5 в качестве транка 802.1Q
