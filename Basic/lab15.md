![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/img/lab%2015-1.jpg?raw=true)

#### Часть 1. Создание сети и настройка основных параметров устройства
##### Шаг 1. Создайте сеть согласно топологии.
##### Шаг 2. Настройте базовые параметры для маршрутизатора.
###### Настройка R1
    Router>enable 
    Router#conf t
    Router(config)#hostname R1
    Router(config)#no ip domain-lookup 
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
    R1(config)#banner motd #!!!#
    R1(config)#interface loopback1
    R1(config-if)#ip address 172.16.1.1 255.255.255.0
    R1(config-if)#no shutdown 
    R1(config-if)#ex
    R1(config)#interface gigabitEthernet 0/0/1
    R1(config-if)#ip address 10.22.0.1 255.255.255.0
    R1(config-if)#no shutdown 
    R1(config-if)#ex
    R1(config)#ex
    R1#wr m
    
##### Шаг 3. Настройка базовых параметров каждого коммутатора. Настройка SVI для VLAN 1 на S1 и S2
###### Настройка на примере S1
    Switch>enable 
    Switch#conf t
    Switch(config)#hostname S1
    S1(config)#no ip domain-lookup 
    S1(config)#enable password class
    S1(config)#service password-encryption 
    S1(config)#line console 0
    S1(config-line)#password cisco
    S1(config-line)#login 
    S1(config-line)#exit
    S1(config)#line vty 0 4
    S1(config-line)#password cisco
    S1(config-line)#exit
    S1(config)#banner motd #!!!#
    S1(config-if-range)#interface range fastEthernet 0/2-4, fastEthernet 0/6-24, gigabitEthernet 0/1-2
    S1(config-if-range)#shutdown 
    S1(config-if-range)#ex
	S1(config)#interface vlan 1
    S1(config-if)#ip address 10.22.0.2 255.255.255.0
    S1(config-if)#no shutdown
    S1(config-if)#ex
    S1(config)#ip default-gateway 10.22.0.1
    S1(config)#ex
    S1#wr m
    

#### Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP
    R1#show cdp 
    Global CDP information:
        Sending CDP packets every 60 seconds
        Sending a holdtime value of 180 seconds
        Sending CDPv2 advertisements is enabled
    
    R1#show cdp interface 
    Vlan1 is administratively down, line protocol is down
      Sending CDP packets every 60 seconds
      Holdtime is 180 seconds
    GigabitEthernet0/0/0 is administratively down, line protocol is down
      Sending CDP packets every 60 seconds
      Holdtime is 180 seconds
    GigabitEthernet0/0/1 is up, line protocol is up
      Sending CDP packets every 60 seconds
      Holdtime is 180 seconds
    GigabitEthernet0/0/2 is administratively down, line protocol is down
      Sending CDP packets every 60 seconds
      Holdtime is 180 seconds
    R1#show cdp en
    R1#show cdp entry S1
    
    Device ID: S1
    Entry address(es): 
      IP address : 10.22.0.2
    Platform: cisco 2960, Capabilities: Switch
    Interface: GigabitEthernet0/0/1, Port ID (outgoing port): FastEthernet0/5
    Holdtime: 179
    
    Version :
    Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
    Technical Support: http://www.cisco.com/techsupport
    Copyright (c) 1986-2013 by Cisco Systems, Inc.
    Compiled Wed 26-Jun-13 02:49 by mnguyen
    
    advertisement version: 2
    Duplex: full
    
    R1#show cdp neighbors 
    Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                      S - Switch, H - Host, I - IGMP, r - Repeater, P - Phone
    Device ID    Local Intrfce   Holdtme    Capability   Platform    Port ID
    S1           Gig 0/0/1        170            S       2960        Fas 0/5
    R1#v

#### Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP
###### Вы полняем lldp run на всех устройствах
    R1#show lldp neighbors 
    Capability codes:
        (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
        (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other
    Device ID           Local Intf     Hold-time  Capability      Port ID
    S1                  Gig0/0/1       120        B               Fa0/5
    
    Total entries displayed: 1
	
#### Часть 4. Настройка NTP
###### Настройки на R1
    R1#show clock 
    *1:10:14.631 UTC Mon Mar 1 1993
    R1#clock set 14:30:00 19 Dec 2025
    R1#show clock 
    14:30:4.236 UTC Fri Dec 19 2025
    R1#conf t
    R1(config)#ntp master 4

###### Настройки на S1
    S1#show clock 
    *1:21:11.491 UTC Mon Mar 1 1993
	S1#conf t 
    S1(config)#ntp server 10.22.0.1
    S1(config)#ex
    S1#show ntp ?
      associations  NTP associations
      status        NTP status
    S1#show ntp status 
    Clock is synchronized, stratum 5, reference is 10.22.0.1
    nominal freq is 250.0000 Hz, actual freq is 249.9990 Hz, precision is 2**24
    reference time is ECC1BD53.0000000B (14:38:11.011 UTC Fri Dec 19 2025)
    clock offset is 0.00 msec, root delay is 0.00  msec
    root dispersion is 10.95 msec, peer dispersion is 0.12 msec.
    loopfilter state is 'CTRL' (Normal Controlled Loop), drift is - 0.000001193 s/s system poll interval is 4, last update was 10 sec ago.
    S1#show clock 
    14:38:15.249 UTC Fri Dec 19 2025



