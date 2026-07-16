## Домашнее задание №1
#### Проектирование сети

![](https://github.com/Adminkzn/Otus-Network-Engineer/blob/main/Pro/Lab1/img/1.jpg?raw=true)

Цель:
распланировать адресное пространство, настроить IP на активных портах для дальнейшей работы над проектом и задокументировать адресацию.

------------

#### Разработаете и задокументируете адресное пространство для лабораторного стенда.


#### 1. Management VLAN

#### Management SVI 

| Device | Interface | IP Address |
|--------|-----------|------------|
| SW2    | VLAN99    | 10.255.1.2/24 |
| SW3    | VLAN99    | 10.255.1.3/24 |
| SW4    | VLAN99    | 10.255.1.252/24 |
| SW5    | VLAN99    | 10.255.1.253/24 |
| SW9    | VLAN99    | 10.255.2.252/24 |
| SW10   | VLAN99    | 10.255.2.253/24 |
| SW29   | VLAN99    | 10.255.3.29/24 |

#### Management SVI Gateway

#### 5. Management Gateway

| Site | VLAN | SW Master | SW Backup | VRRP VIP | IP |
|------|------|-----------|-----------|----------|----------|
| MSK | 99 | SW4 - 10.255.1.252 | SW5 - 10.255.1.253 | 10.255.1.254 | - |
| SPB | 99 | SW9 - 10.255.2.252 | SW10 - 10.255.2.253 | 10.255.2.254 | - |
| CHKD | 99 | - | - | - | 10.255.3.254 |
------------

#### 2. Loopback 

| R | Interface | IP Address     |
|---------|-----------|----------------|
| R12     | Lo0       | 10.255.0.12/32 |
| R13     | Lo0       | 10.255.0.13/32 |
| R14     | Lo0       | 10.255.0.14/32 |
| R15     | Lo0       | 10.255.0.15/32 |
| R16     | Lo0       | 10.255.0.16/32 |
| R17     | Lo0       | 10.255.0.17/32 |
| R18     | Lo0       | 10.255.0.18/32 |
| R19     | Lo0       | 10.255.0.19/32 |
| R20     | Lo0       | 10.255.0.20/32 |
| R21     | Lo0       | 10.255.0.21/32 |
| R22     | Lo0       | 10.255.0.22/32 |
| R23     | Lo0       | 10.255.0.23/32 |
| R24     | Lo0       | 10.255.0.24/32 |
| R25     | Lo0       | 10.255.0.25/32 |
| R26     | Lo0       | 10.255.0.26/32 |
| R27     | Lo0       | 10.255.0.27/32 |
| R28     | Lo0       | 10.255.0.28/32 |
| R32     | Lo0       | 10.255.0.32/32 |
------------

#### 3. Office VLAN
| Офис            | VLAN | Network         | Gateway        |
|-----------------|-----:|-----------------|----------------|
| MSK | 10   | 192.168.10.0/24 | 192.168.10.254   |
| SPB | 20   | 192.168.20.0/24 | 192.168.20.254   |
| CHKD | 30   | 192.168.30.0/24 | 192.168.30.254   |
------------

#### 4. VRRP

| Site | VRRP Group | VLAN | Virtual IP | Master Device | Master IP | Priority | Backup Device | Backup IP | Priority |
|------|-----------|------|------------|--------------|-----------|----------|--------------|-----------|----------|
| MSK | 10 | 10 | 192.168.10.254 | SW4 | 192.168.10.252 | 110 | SW5 | 192.168.10.253 | 100 |
| MSK | 99 | 99 | 10.255.1.254 | SW4 | 10.255.1.252 | 110 | SW5 | 10.255.1.253 | 100 |
| SPB | 20 | 20 | 192.168.20.254 | SW9 | 192.168.20.252 | 110 | SW10 | 192.168.20.253 | 100 |
| SPB | 99 | 99 | 10.255.2.254 | SW9 | 10.255.2.252 | 110 | SW10 | 10.255.2.253 | 100 |

| Office | Gateway |
|------|---------|
| CHKD | 10.255.3.254 (R28) |
------------

#### 5. VPC
| Device | VLAN | IP Address      | Gateway      |
|--------|-----:|-----------------|--------------|
| VPC1   | 10   | 192.168.10.10   | 192.168.10.254 |
| VPC7   | 10   | 192.168.10.11   | 192.168.10.254 |
| VPC8   | 20   | 192.168.20.10   | 192.168.20.254 |
| VPC    | 20   | 192.168.20.11   | 192.168.20.254 |
| VPC30  | 30   | 192.168.30.10   | 192.168.30.254 |
| VPC31  | 30   | 192.168.30.11   | 192.168.30.254 |
------------

#### 6. Point-to-Point Networks

| Device A - Device B | Network | Device A | Device B |
|---------------------|---------|----------|----------|
| R12-R14 | 10.0.0.0/30 | 10.0.0.1 | 10.0.0.2 |
| R13-R15 | 10.0.0.4/30 | 10.0.0.5 | 10.0.0.6 |
| R13-R14 | 10.0.0.8/30 | 10.0.0.9 | 10.0.0.10 |
| R12-R15 | 10.0.0.12/30 | 10.0.0.13 | 10.0.0.14 |
| R14-R22 | 10.0.0.16/30 | 10.0.0.17 | 10.0.0.18 |
| R15-R21 | 10.0.0.20/30 | 10.0.0.21 | 10.0.0.22 |
| R21-R22 | 10.0.0.24/30 | 10.0.0.25 | 10.0.0.26 |
| R22-R23 | 10.0.0.28/30 | 10.0.0.29 | 10.0.0.30 |
| R21-R24 | 10.0.0.32/30 | 10.0.0.33 | 10.0.0.34 |
| R23-R25 | 10.0.0.36/30 | 10.0.0.37 | 10.0.0.38 |
| R24-R26 | 10.0.0.40/30 | 10.0.0.41 | 10.0.0.42 |
| R25-R27 | 10.0.0.44/30 | 10.0.0.45 | 10.0.0.46 |
| R26-R28 | 10.0.0.48/30 | 10.0.0.49 | 10.0.0.50 |
| R25-R26 | 10.0.0.52/30 | 10.0.0.53 | 10.0.0.54 |
| R23-R24 | 10.0.0.56/30 | 10.0.0.57 | 10.0.0.58 |
| R18-R24 | 10.0.0.60/30 | 10.0.0.61 | 10.0.0.62 |
| R18-R26 | 10.0.0.64/30 | 10.0.0.65 | 10.0.0.66 |
| R25-R28 | 10.0.0.68/30 | 10.0.0.69 | 10.0.0.70 |
| R15-R20 | 10.0.0.72/30 | 10.0.0.73 | 10.0.0.74 |
| R14-R19 | 10.0.0.76/30 | 10.0.0.77 | 10.0.0.78 |
| R16-R18 | 10.0.0.80/30 | 10.0.0.81 | 10.0.0.82 |
| R17-R18 | 10.0.0.84/30 | 10.0.0.85 | 10.0.0.86 |
| R16-R32 | 10.0.0.88/30 | 10.0.0.89 | 10.0.0.90 |
| SW4-R12 | 10.0.0.92/30 | 10.0.0.93 | 10.0.0.94 |
| SW4-R13 | 10.0.0.96/30 | 10.0.0.97 | 10.0.0.98 |
| SW5-R12 | 10.0.0.100/30 | 10.0.0.101 | 10.0.0.102 |
| SW5-R13 | 10.0.0.104/30 | 10.0.0.105 | 10.0.0.106 |
| SW9-R16 | 10.0.0.108/30 | 10.0.0.109 | 10.0.0.110 |
| SW9-R17 | 10.0.0.112/30 | 10.0.0.113 | 10.0.0.114 |
| SW10-R16 | 10.0.0.116/30 | 10.0.0.117 | 10.0.0.118 |
| SW10-R17 | 10.0.0.120/30 | 10.0.0.121 | 10.0.0.122 |
------------

#### 6. Настройки
<!-- ================================================================================================================ -->
<details>
<summary><strong>Настройка SW2</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW2
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! VLAN
! =========================
vlan 10
 name MSK_USERS
 exit

vlan 99
 name MSK_MANAGEMENT
 exit

! =========================
! MANAGEMENT
! =========================
interface Vlan99
 description MSK_MANAGEMENT VLAN99
 ip address 10.255.1.2 255.255.255.0
 no shutdown
 exit

ip default-gateway 10.255.1.254

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/0
 description TRUNK_TO_SW5
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 exit

interface Ethernet0/1
 description TRUNK_TO_SW4
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 exit

! =========================
! ACCESS PORTS
! =========================
interface Ethernet0/2
 description VPC7
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit

! =========================
! UNUSED PORTS
! =========================
interface range Ethernet0/3,Ethernet1/0-3
 description UNUSED
 shutdown
 exit

spanning-tree mode rapid-pvst

end
copy running-config startup-config
```

</details>

<!-- ================================================================================================================ -->
<!-- ================================================================================================================ -->

<details>
<summary><strong>Настройка SW3</strong></summary>
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW3
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit
 
! =========================
! VLAN
! =========================
vlan 10
 name MSK_USERS
 exit
vlan 99
 name MSK_MANAGEMENT
 exit
! =========================
! MANAGEMENT
! =========================
interface Vlan99
 description MSK_MANAGEMENT
 ip address 10.255.1.3 255.255.255.0
 no shutdown
 exit

ip default-gateway 10.255.1.254

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/0
 description TRUNK_TO_SW4
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 exit
 
interface Ethernet0/1
 description TRUNK_TO_SW5
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 exit
 
! =========================
! ACCESS PORTS
! =========================
interface Ethernet0/2
 description VPC1
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit


! =========================
! UNUSED PORTS
! =========================
interface range Ethernet0/3,Ethernet1/0-3
 description UNUSED
 shutdown
 exit

spanning-tree mode rapid-pvst
end
copy running-config startup-config

</details>

<!-- ================================================================================================================ -->
<!-- ================================================================================================================ -->

<details>
<summary><strong>Настройка SW4</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW4
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! L3 SWITCHING
! =========================
ip routing

! =========================
! VLAN 
! =========================
vlan 10
 name MSK_USERS
 exit

vlan 99
 name MSK_MANAGEMENT
 exit

! =========================
! SVI + VRRP
! =========================
interface Vlan10
 description MSK_USERS
 ip address 192.168.10.252 255.255.255.0
 vrrp 10 ip 192.168.10.254
 vrrp 10 priority 110
 vrrp 10 preempt
 no shutdown
 exit

interface Vlan99
 description MSK_MANAGEMENT
 ip address 10.255.1.252 255.255.255.0
 vrrp 99 ip 10.255.1.254
 vrrp 99 priority 110
 vrrp 99 preempt
 no shutdown
 exit

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/0
 description TRUNK_TO_SW3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

interface Ethernet0/1
 description TRUNK_TO_SW2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

interface Ethernet0/2
 description TRUNK_TO_SW5
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

interface Ethernet0/3
 description TRUNK_TO_SW5
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet1/0
 description TO_R12
 no switchport
 ip address 10.0.0.93 255.255.255.252
 no shutdown
 exit

interface Ethernet1/1
 description TO_R13
 no switchport
 ip address 10.0.0.97 255.255.255.252
 no shutdown
 exit

! =========================
! UNUSED PORTS
! =========================
interface range Ethernet1/2-3
 description UNUSED
 shutdown
 exit

! =========================
! SPANNING TREE
! =========================
spanning-tree mode rapid-pvst
spanning-tree vlan 10,99 priority 16384

end
copy running-config startup-config
```

</details>

<!-- ================================================================================================================ -->
<!-- ================================================================================================================ -->

<details>
<summary><strong>Настройка SW5</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW5
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! L3 SWITCHING
! =========================
ip routing

! =========================
! VLAN 
! =========================
vlan 10
 name MSK_USERS
 exit

vlan 99
 name MSK_MANAGEMENT
 exit

! =========================
! SVI + VRRP
! =========================
interface Vlan10
 description MSK_USERS
 ip address 192.168.10.253 255.255.255.0
 vrrp 10 ip 192.168.10.254
 vrrp 10 priority 100
 vrrp 10 preempt
 no shutdown
 exit

interface Vlan99
 description MSK_MANAGEMENT
 ip address 10.255.1.253 255.255.255.0
 vrrp 99 ip 10.255.1.254
 vrrp 99 priority 100
 vrrp 99 preempt
 no shutdown
 exit

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/0
 description TRUNK_TO_SW2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

interface Ethernet0/1
 description TRUNK_TO_SW3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

interface Ethernet0/2
 description TRUNK_TO_SW4
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

interface Ethernet0/3
 description TRUNK_TO_SW4
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,99
 no shutdown
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet1/0
 description TO_R13
 no switchport
 ip address 10.0.0.105 255.255.255.252
 no shutdown
 exit

interface Ethernet1/1
 description TO_R12
 no switchport
 ip address 10.0.0.101 255.255.255.252
 no shutdown
 exit

! =========================
! UNUSED PORTS
! =========================
interface range Ethernet1/2-3
 description UNUSED
 shutdown
 exit

! =========================
! SPANNING TREE
! =========================
spanning-tree mode rapid-pvst
spanning-tree vlan 10,99 priority 24576

end
copy running-config startup-config
```

</details>

<!-- ================================================================================================================ -->
<!-- ================================================================================================================ -->

<details>
<summary><strong>Настройка SW9</strong></summary>

```cisco

!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW9
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! L3 SWITCHING
! =========================
ip routing

! =========================
! VLAN
! =========================
vlan 20
 name SPB_USERS
 exit
vlan 99
 name SPB_MANAGEMENT
 exit

! =========================
! SVI + VRRP
! =========================
interface Vlan20
 description SPB_USERS
 ip address 192.168.20.252 255.255.255.0
 vrrp 20 ip 192.168.20.254
 vrrp 20 priority 110
 vrrp 20 preempt
 no shutdown
 exit

interface Vlan99
 description SPB_MANAGEMENT
 ip address 10.255.2.252 255.255.255.0
 vrrp 99 ip 10.255.2.254
 vrrp 99 priority 110
 vrrp 99 preempt
 no shutdown
 exit

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/0
 description TRUNK_TO_SW10
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,99
 exit
 
interface Ethernet0/1
 description TRUNK_TO_SW10
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,99
 exit
 
! =========================
! ACCESS PORTS
! =========================
interface Ethernet0/2
 description VPC8
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit
 
! =========================
! UPLINKS
! =========================
interface Ethernet1/0
 description TO_R16
 no switchport
 ip address 10.0.0.109 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R17
 no switchport
 ip address 10.0.0.113 255.255.255.252
 no shutdown
 exit

! =========================
! UNUSED PORTS
! =========================
interface range Ethernet1/2-3
 description UNUSED
 shutdown
 exit

spanning-tree mode rapid-pvst
spanning-tree vlan 20,99 priority 16384
end
copy running-config startup-config

```
</details>

<!-- ================================================================================================================ -->
<!-- ================================================================================================================ -->

<details>
<summary><strong>Настройка SW10</strong></summary>

```cisco

!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW10
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! L3 SWITCHING
! =========================
ip routing

 
! =========================
! VLAN
! =========================
vlan 20
 name SPB_USERS
 exit
vlan 99
 name SPB_MANAGEMENT
 exit

! =========================
! SVI + VRRP
! =========================
interface Vlan20
 description SPB_USERS
 ip address 192.168.20.253 255.255.255.0
 vrrp 20 ip 192.168.20.254
 vrrp 20 priority 100
 vrrp 20 preempt
 no shutdown
 exit

interface Vlan99
 description SPB_MANAGEMENT
 ip address 10.255.2.253 255.255.255.0
 vrrp 99 ip 10.255.2.254
 vrrp 99 priority 100
 vrrp 99 preempt
 no shutdown
 exit 

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/0
 description TRUNK_TO_SW9
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,99
 exit
 
interface Ethernet0/1
 description TRUNK_TO_SW9
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20,99
 exit
 
! =========================
! ACCESS PORTS
! =========================
interface Ethernet0/2
 description VPC
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit
 
! =========================
! UPLINKS
! =========================
interface Ethernet1/0
 description TO_R17
 no switchport
 ip address 10.0.0.121 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R16
 no switchport
 ip address 10.0.0.117 255.255.255.252
 no shutdown
 exit 

! =========================
! UNUSED PORTS
! =========================
interface range Ethernet1/2-3
 description UNUSED
 shutdown
 exit

spanning-tree mode rapid-pvst
spanning-tree vlan 20,99 priority 24576
end
copy running-config startup-config

```
</details>

<!-- ================================================================================================================ -->
<!-- ================================================================================================================ -->

<details>
<summary><strong>Настройки SW29</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname SW29
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! VLAN
! =========================
vlan 30
 name CHKD
 exit

vlan 99
 name MANAGEMENT
 exit

! =========================
! MANAGEMENT
! =========================
interface Vlan99
 description Management
 ip address 10.255.3.29 255.255.255.0
 no shutdown
 exit

ip default-gateway 10.255.3.254

! =========================
! TRUNK PORTS
! =========================
interface Ethernet0/2
 description TRUNK_TO_R28
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 30,99
 exit

! =========================
! ACCESS PORTS
! =========================
interface Ethernet0/0
 description VPC30
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit

interface Ethernet0/1
 description VPC31
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit

! =========================
! UNUSED PORTS
! =========================
interface Ethernet0/3
 description UNUSED
 shutdown
 exit

spanning-tree mode rapid-pvst
spanning-tree vlan 30,99 priority 24576

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R12</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R12
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.12 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/2
 description TO_R14
 ip address 10.0.0.1 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/3
 description TO_R15
 ip address 10.0.0.13 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/0
 description TO_SW4
 ip address 10.0.0.94 255.255.255.252
 no shutdown
 exit

interface Ethernet0/1
 description TO_SW5
 ip address 10.0.0.102 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R13</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R13
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.13 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/2
 description TO_R15
 ip address 10.0.0.5 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/3
 description TO_R14
 ip address 10.0.0.9 255.255.255.252
 no shutdown
 exit

interface Ethernet0/0
 description TO_SW4
 ip address 10.0.0.98 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_SW5
 ip address 10.0.0.106 255.255.255.252
 no shutdown
 exit
end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R14</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R14
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.14 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R12
 ip address 10.0.0.2 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R13
 ip address 10.0.0.10 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R22
 ip address 10.0.0.17 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R19
 ip address 10.0.0.77 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R15</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R15
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.15 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R13
 ip address 10.0.0.6 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R12
 ip address 10.0.0.14 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R21
 ip address 10.0.0.21 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R20
 ip address 10.0.0.73 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R16</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R16
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.16 255.255.255.255
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet0/1
 description TO_R18
 ip address 10.0.0.81 255.255.255.252
 no shutdown
 exit
 
! =========================
! P2P LINKS
! =========================
interface Ethernet0/3
 description TO_R32
 ip address 10.0.0.89 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/0
 description TO_SW10
 ip address 10.0.0.118 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/2
 description TO_SW9
 ip address 10.0.0.110 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R17</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R17
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.17 255.255.255.255
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet0/1
 description TO_R18
 ip address 10.0.0.85 255.255.255.252
 no shutdown
 exit
 
! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_SW9
 ip address 10.0.0.114 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/2
 description TO_SW10
 ip address 10.0.0.122 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R18</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R18
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.18 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R16
 ip address 10.0.0.82 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R17
 ip address 10.0.0.86 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R24
 ip address 10.0.0.61 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R26
 ip address 10.0.0.65 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройки R19</strong></summary>

```cisco
!=========================
! BASIC CONFIGURATION
!=========================
hostname R19
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE & SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.19 255.255.255.255
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet0/0
 description TO_R14
 ip address 10.0.0.78 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R20</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R20
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.20 255.255.255.255
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet0/0
 description TO_R15
 ip address 10.0.0.74 255.255.255.252
 no shutdown
 exit
 
interface range Ethernet0/1-3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>
<details>
<summary><strong>Настройка R21</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R21
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.21 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R15
 ip address 10.0.0.22 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R22
 ip address 10.0.0.25 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R24
 ip address 10.0.0.33 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R22</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R22
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.22 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R14
 ip address 10.0.0.18 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R21
 ip address 10.0.0.26 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R23
 ip address 10.0.0.29 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R23</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R23
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.23 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R22
 ip address 10.0.0.30 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R25
 ip address 10.0.0.37 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R24
 ip address 10.0.0.57 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>



<details>
<summary><strong>Настройка R24</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R24
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.24 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R21
 ip address 10.0.0.34 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R26
 ip address 10.0.0.41 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R23
 ip address 10.0.0.58 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R18
 ip address 10.0.0.62 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R25</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R25
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.25 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R23
 ip address 10.0.0.38 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R27
 ip address 10.0.0.45 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R26
 ip address 10.0.0.53 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R28
 ip address 10.0.0.69 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R26</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R26
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.26 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R24
 ip address 10.0.0.42 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R28
 ip address 10.0.0.49 255.255.255.252
 no shutdown
 exit

interface Ethernet0/2
 description TO_R25
 ip address 10.0.0.54 255.255.255.252
 no shutdown
 exit

interface Ethernet0/3
 description TO_R18
 ip address 10.0.0.66 255.255.255.252
 no shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R27</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R27
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.27 255.255.255.255
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet0/0
 description TO_R25
 ip address 10.0.0.46 255.255.255.252
 no shutdown
 exit
 
interface range Ethernet0/1-3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R28</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R28
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.28 255.255.255.255
 exit

! =========================
! P2P LINKS
! =========================
interface Ethernet0/0
 description TO_R26
 ip address 10.0.0.50 255.255.255.252
 no shutdown
 exit
 
interface Ethernet0/1
 description TO_R25
 ip address 10.0.0.70 255.255.255.252
 no shutdown
 exit

! =========================
! OFFICE TRUNK
! =========================
interface Ethernet0/2
 description TRUNK_TO_SW29
 no shutdown
 exit

! =========================
! USER VLANs
! =========================
interface Ethernet0/2.30
 description CHKD_USERS
 encapsulation dot1Q 30
 ip address 192.168.30.254 255.255.255.0
 exit

interface Ethernet0/2.99
 description CHKD_MANAGEMENT
 encapsulation dot1Q 99
 ip address 10.255.3.254 255.255.255.0
 exit

interface Ethernet0/3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>

<details>
<summary><strong>Настройка R32</strong></summary>

```cisco
!=========================
! БАЗОВАЯ НАСТРОЙКА
!=========================
hostname R32
no ip domain-lookup
enable secret admin
service password-encryption
username admin privilege 15 secret admin
ip domain-name otus.ru
crypto key generate rsa general-keys modulus 2048
ip ssh version 2
banner motd # OTUS LAB - Authorized access only #

! =========================
! CONSOLE&&SSH
! =========================
line console 0
 login local
 exec-timeout 10 0
 logging synchronous
 exit

line vty 0 4
 login local
 transport input ssh
 exec-timeout 10 0
 logging synchronous
 exit

! =========================
! LOOPBACK
! =========================
interface Loopback0
 description ROUTER_ID
 ip address 10.255.0.32 255.255.255.255
 exit

! =========================
! UPLINKS
! =========================
interface Ethernet0/0
 description TO_R16
 ip address 10.0.0.90 255.255.255.252
 no shutdown
 exit
 
interface range Ethernet0/1-3
 description UNUSED
 shutdown
 exit

end
copy running-config startup-config
```

</details>

------------
