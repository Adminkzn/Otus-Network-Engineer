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
Базовая настройка R1 и R2 одинакова 

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
**a.**

     R2(config)#interface gigabitEthernet 0/0/1
     R2(config-if)#ip address 192.168.1.97 255.255.255.240
     R2(config-if)#no shutdown

**b, с**
    
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

**d**
    
    R1#ping 10.0.0.2
    
    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 10.0.0.2, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms
    
    R1#ping 192.168.1.97
    
    Type escape sequence to abort.
    Sending 5, 100-byte ICMP Echos to 192.168.1.97, timeout is 2 seconds:
    !!!!!
    Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms
    
**e**

    R1#copy running-config startup-config 
    
#### Шаг 6.	Настройте базовые параметры каждого коммутатора
Базовые настройки S1 и S2 одинакова 

    Switch>
    Switch>enable
    Switch#conf t
    Enter configuration commands, one per line.  End with CNTL/Z.
    Switch(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#service password-encryption 
    S1(config)#enable secret class
    S1(config)#banner motd #!!!ACCESS DENIED!!!#
    S1(config)#line console 0
    S1(config-line)#logging synchronous 
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#exec-timeout 10 0
    S1(config-line)#exit
    S1(config)#line vty 0 4
    S1(config-line)#logging synchronous 
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#exec-timeout 10 0
    S1(config-line)#exit
    S1(config)#exit
    S1#clock set 8:50:00 17 november 2025 
    S1#copy running-config startup-config
    %SYS-5-CONFIG_I: Configured from console by console
    S1#copy running-config startup-config
    Destination filename [startup-config]? 
    Building configuration...
    [OK]
    S1#
	

#### Шаг 7.	Создайте сети VLAN на коммутаторе S1
**a,b**

    S1(config)#vlan 100
    S1(config-vlan)#nam
    S1(config-vlan)#name  Client
    S1(config-vlan)#exit 
    S1(config)#vlan 200
    S1(config-vlan)#name Management
    S1(config-vlan)#exit 
    S1(config)#vlan 999
    S1(config-vlan)#name Parking_Lot
    S1(config-vlan)#exit 
    S1(config)#vlan 1000
    S1(config-vlan)#name Native
    S1(config-vlan)#exit
    S1(config)#interface fastEthernet 0/6
    S1(config-if)#switchport mode access 
    S1(config-if)#switchport access vlan 100
    S1(config-if)#description PC-A
    S1(config-if)#no shutdown 
    S1(config-if)#exit 
    S1(config)#interface vlan 200
    S1(config-if)#ip address 192.168.1.66 255.255.255.224
    S1(config-if)#no shutdown 
    S1(config-if)#exit 
    S1(config)#ip default-gateway 192.168.1.65

**c.**

    S2#conf t
    S2(config)#interface vlan 1
    S2(config-if)#ip address 192.168.1.98 255.255.255.240
    S2(config-if)#no shutdown
    S2(config-if)#exit
    S2(config)#ip default-gateway 192.168.1.97
	
**d.**

**S1**
	
    	S1(config)#interface range f0/1-4, f0/7-24, g0/1-2
        S1(config-if-range)#switchport mode access
        S1(config-if-range)#switchport access vlan 999
        S1(config-if-range)#shutdown
        S1(config-if-range)#exit
		
**S2**

    S2(config)#interface range f0/1-17, f0/19-24, g0/1-2
    S2(config-if-range)#shutdown
	S1(config-if-range)#exit
	S2(config)#interface fastEthernet 0/5
	S2(config-if)#no shutdown 
	S1(config-if-range)#exit
	


    
#### Шаг 8.	Назначьте сети VLAN соответствующим интерфейсам коммутатора
#### Шаг 9.	Вручную настройте интерфейс S1 F0/5 в качестве транка 802.1Q
