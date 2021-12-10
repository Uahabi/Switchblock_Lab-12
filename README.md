# -----   -Switchblock_Lab-12-   ------
Labo Cours de Technologies réseaux et commutations

# *** Commande exécuté dans le labo ***

# 1* VPCS :

# PC110
ip 10.0.0.110 255.255.255.0 10.0.0.1

wr

# PC120
ip 10.0.0.120 255.255.255.0 10.0.0.1

wr

# PC130
ip 10.0.1.130 255.255.255.0 10.0.1.1

wr

# PC140
ip 10.0.1.140 255.255.255.0 10.0.1.1

wr

# PC210
ip 10.0.0.210 255.255.255.0 10.0.0.1

wr

# PC220
ip 10.0.0.220 255.255.255.0 10.0.0.1

wr

# PC230
ip 10.0.1.230 255.255.255.0 10.0.1.1

wr

# PC240
ip 10.0.1.240 255.255.255.0 10.0.1.1

wr

# 2* Switch:

# AS1

enable 
Configure terminal
vlan 10
name HR
vlan 20
name Engineering

interface GigabitEthernet2/0
Switchport mode access
Switchport access vlan 10
switchport host

interface GigabitEthernet2/1
Switchport mode access
Switchport access vlan 10
switchport host

interface GigabitEthernet2/2
Switchport mode access
Switchport access vlan 20
switchport host

interface GigabitEthernet2/3
Switchport mode access
Switchport access vlan 20
switchport host

interface GigabitEthernet0/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet0/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
  switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
do wr

# AS2

enable 
Configure terminal
vlan 10
name HR
vlan 20
name Engineering

interface GigabitEthernet2/0
Switchport mode access
Switchport access vlan 10
switchport host

interface GigabitEthernet2/1
Switchport mode access
Switchport access vlan 10
switchport host

interface GigabitEthernet2/2
Switchport mode access
Switchport access vlan 20
switchport host

interface GigabitEthernet2/3
Switchport mode access
Switchport access vlan 20
switchport host

interface GigabitEthernet0/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet0/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
  switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
 do wr
 
# DS1
 
enable 
Configure terminal
vlan 10
name HR
vlan 20
name Engineering

 interface GigabitEthernet0/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet0/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet0/2
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/2
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20

# DS2 :

enable 
Configure terminal
vlan 10
name HR
vlan 20
name Engineering
 
 interface GigabitEthernet0/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet0/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet0/2
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/0
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/1
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 interface GigabitEthernet1/2
    switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 
> DS2=> R1

enable
conf t
interface GigabitEthernet3/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20
description DS2 to R1
 
# 3* Routeur :

> R1 => DS2

enable
conf t
interface GigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 10.0.0.1 255.255.255.0
!
interface GigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 10.0.1.1 255.255.255.0
description R1 to DS2
activation du dhcp
 
# Activation du service DHCP

ip dhcp pool vlan10
network 10.0.0.0 255.255.255.0
default-router 10.0.0.1

# Aggrégation de lien (Etherchannel) sur Switch de distribution DS1 et DS2

enable
conf t
Interface range  G0/0-1
channel-group 1 mode desirable
interface port-channel 1
no shut
