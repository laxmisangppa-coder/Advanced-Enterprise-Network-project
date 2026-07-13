# Advanced-Enterprise-Network-project

COMMANDS IN CLI(COMMAND LINE INTERFACE)

1) IP CONFIGURATION OF PC's

VLAN1
Pc1
Ipv4 address: 192.168.10.10
Subnet mask: 255.255.255.0
Default gateway: 192.168.10.100
Dns server: 0.0.0.0

Pc2
Ipv4 address: 192.168.10.20
Subnet mask: 255.255.255.0
Default gateway: 192.168.10.100
Dns server: 0.0.0.0

VLAN2
Pc3
Ipv4 address: 192.168.20.10
Subnet mask: 255.255.255.0
Default gateway: 192.168.20.100
Dns server: 0.0.0.0

Pc4
Ipv4 address: 192.168.20.20
Subnet mask: 255.255.255.0
Default gateway: 192.168.20.100
Dns server: 0.0.0.0

VLAN 3
Pc5
Ipv4 address: 192.168.30.10
Subnet mask: 255.255.255.0
Default gateway: 192.168.30.100
Dns server: 0.0.0.0

Pc6
Ipv4 address: 192.168.30.20
Subnet mask: 255.255.255.0
Default gateway: 192.168.30.100
Dns server: 0.0.0.0


2) ACCESS LAYER SWITCH's(single access switch)

SWITCH1
Switch> enable
Switch# configure terminal
Switch(config)# int range f0/3-4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# ctrl+z
Switch# show vlan brief

SWITCH2
Switch> enable
Switch# configure terminal
Switch(config)# int range f0/3-4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# ctrl+z
Switch# show vlan brief

SWITCH3
Switch> enable
Switch# configure terminal
Switch(config)# int range f0/3-4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 30
Switch(config-if-range)# ctrl+z
Switch# show vlan brief


3)DISTRIBUTION LAYER SWITCH's(multilayer switch)

TRUNK CONFIGURATION:

SWITCH1
Would you like to enter the initial configuration dialog? [yes/no] : no
Switch> enable
Switch# show interfaces trunk
Switch# configure terminal
Switch(config)# int range f0/2-4
Switch(config-if-range)# switchport mode dynamic desirable
Switch(config-if-range)# ctrl+z
Switch# show interface trunk


SWITCH2
Would you like to enter the initial configuration dialog? [yes/no] : no
Switch> enable
Switch# show interfaces trunk
Switch# configure terminal
Switch(config)# int range f0/2-4
Switch(config-if-range)# switchport mode dynamic desirable
Switch(config-if-range)# ctrl+z
Switch# show interface trunk


4) CREATE SVI 

SWITCH1
Switch# hostname sw1
Switch(config)# vlan 10
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# exit
Switch(config)# vlan 30
Switch(config-vlan)# exit

Switch(config)# int vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# exit

Switch(config)# int vlan 20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
Switch(config-if)# exit

Switch(config)# int vlan 30
Switch(config-if)# ip address 192.168.30.1 255.255.255.0
Switch(config-if)# exit
Switch# show ip interface brief

Check ......
Switch# ping 192.168.30.1
Switch# ping 192.168.20.2
Switch# ping 192.168.10.1

SWITCH2
Switch# hostname sw2
Switch(config)# vlan 10
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# exit
Switch(config)# vlan 30
Switch(config-vlan)# exit

Switch(config)# int vlan 10
Switch(config-if)# ip address 192.168.10.2 255.255.255.0
Switch(config-if)# exit

Switch(config)# int vlan 20
Switch(config-if)# ip address 192.168.20.2 255.255.255.0
Switch(config-if)# exit

Switch(config)# int vlan 30
Switch(config-if)# ip address 192.168.30.2 255.255.255.0
Switch(config-if)# exit
Switch# show ip interface brief

Check ........
Switch# ping 192.168.30.1
Switch# ping 192.168.20.2
Switch# ping 192.168.10.1


5) CONFIGURING HSRP

Note:
Virtual ip add for vlan 10 : 192.168.10.100
Virtual ip add for vlan 20 : 192.168.20.100
Virtual ip add for vlan 30 : 192.168.30.100

SWITCH1
Switch(config)# int vlan 10
Switch(config-if)# standby 10 priority 110
Switch(config-if)# standby 10 preempt
Switch(config-if)# standby ip 192..168.10.100
SWITCH2
Switch(config)# int vlan 10
Switch(config-if)# standby 10 preempt
Switch(config-if)# standby ip 192..168.10.100
Switch# show standby


SWITCH1
Switch(config)# int vlan 20
Switch(config-if)# standby 10 priority 110
Switch(config-if)# standby 10 preempt
Switch(config-if)# standby ip 192..168.20.100
SWITCH2
Switch(config)# int vlan 20
Switch(config-if)# standby 10 preempt
Switch(config-if)# standby ip 192..168.20.100
Switch# show standby

SWITCH1
Switch(config)# int vlan 30
Switch(config-if)# standby 10 priority 110
Switch(config-if)# standby 10 preempt
Switch(config-if)# standby ip 192..168.30.100
SWITCH2
Switch(config)# int vlan 30
Switch(config-if)# standby 10 preempt
Switch(config-if)# standby ip 192..168.30.100
Switch# show standby


CHECK .........
On pc1-
ping  192.168.10.100
ping  192.168.20.100
ping  192.168.30.100

On pc4-
ping  192.168.10.100
ping  192.168.20.100
ping  192.168.30.100

On pc5-
ping  192.168.10.100
ping  192.168.20.100
ping  192.168.30.100


6) MAKE LAYER 2 SWITCH TO LAYER 3 SWITCH

SWITCH1
Switch(config)# ip routing
Switch(config)# int f0/1
Switch(config-if)#no switchport
Switch(config-if)# ip address 10.10.10.1 255.255.255.252
Switch(config-if)# no shutdown
Switch(config-if)# exit

SWITCH2
Switch(config)# ip routing
Switch(config)# int f0/1
Switch(config-if)#no switchport
Switch(config-if)# ip address 10.10.10.5 255.255.255.252
Switch(config-if)# no shutdown
Switch(config-if)# exit


7) CONFIGURATION ON ROUTER

Router> enable
Router# configure terminal
Router(config)# int f0/0 
Router(config-if)# no shutdown 
Router(config-if)# ip address  10.10.10.2 255.255.255.252
Router(config-if)# exit
Router(config)# int f0/1
Router(config-if)# no shutdown
Router(config-if)# ip address 10.10.10.6 255.255.255.252
Router(config-if)# exit

Router(config)# int s0/0/0
Router(config-if)# no shutdown
Router(config-if)# ip address 100.1.1.1 255.255.255.252 
Router(config-if)# exit


8) INTERNET ROUTER

Router> enable
Router# configure terminal
Router(config)# int s0/2/0
Router(config-if)# no shutdown
Router(config-if)# ip address 100.1.1.2 255.255.255.252
Router(config)# exit

Router(config)# int s0/2/1
Router(config-if)# no shutdown
Router(config-if)# ip address 101.1.1.2 255.255.255.252
Router(config-if)# exit

Router(config)# int 11
Router(config-if)# ip address 8.8.8.8 255.255.255.255
Router(config-if)# ctrl+z
Router# show ip interface brief



9) OSPF CONFIGURATION

SWITCH1
Switch(config)# router ospf 1
Switch(config-router)#  network 10.10.10.1 0.0.0.0 area 0
Switch(config-router)#  network 192.168.10.0 0.0.0.255 area 0
Switch(config-router)#  network 192.168.20.0 0.0.0.255 area 0
Switch(config-router)#  network 192.168.30.0 0.0.0.255 area 0
Switch(config-router)#  ctrl+z
Switch# show ip ospt interface brief


ROUTER 1
Router(config-router)# router ospf 1
Router(config-router)# network 10.10.10.2 0.0.0.0 area 0
Router(config-router)# ctrl+Z
Router# show ip ospf neighbor
Router# show ip route ospf

SWITCH2
Switch(config)# router ospf 1
Switch(config-router)#  network 10.10.10.5 0.0.0.0 area 0
Switch(config-router)#  network 192.168.10.0 0.0.0.255 area 0
Switch(config-router)#  network 192.168.20.0 0.0.0.255 area 0
Switch(config-router)#  network 192.168.30.0 0.0.0.255 area 0
Switch(config-router)#  ctrl+z
Switch# show ip ospt interface brief
Switch# show ip ospf neighbor

ROUTER1
Router(config)#  int f0/1
Router(config-if)# ip ospf 1 area 0
Router(config-if)# ctrl+z
Router# show ip ospf neighbor 
Router# show ip route

SWITCH1
Switch# show ip ospf neighbor
Switch(config)# int vlan 10
Switch(config-if)# exit
Switch(config)# router ospf 1
Switch(config-router)# passive-interface vlan 10
Switch(config-router)# passive-interface vlan 20
Switch(config-router)# passive-interface vlan 30
Switch# show ip ospf neighbor
Switch# show ip route ospf

SWITCH2
Switch(config)# router ospf 1
Switch(config-router)# passive-interface vlan 10
Switch(config-router)# passive-interface vlan 20
Switch(config-router)# passive-interface vlan 30
Switch# show ip ospf neighbor
Switch# show ip route ospf


[done the LAN network]



[let's start NAT]...........

ROUTER1
Router(config)# ip route 0.0.0.0 0.0.0.0 100.1.1.2
Router(config)# ctrl+z
Router# hostname r1
Router(config)# access-list 10 permit 192.168.0.0 0.0.255.255
Router(config)# ip nat inside source list 10 int s0/0/0 overload
Router(config)# router ospf 1
Router(config-router)# default-information originate
Router(config)# ctrl+z
 
Check
Sw1# show ip route
Sw2# show ip route ospf
R1# show access-lists
R1#show ip nat traslations
R1# show running-config

ROUTER1
Router(config)# int s0/0/0
Router(config-if)# ip nat outside
Router(config-if)# exit
Router(config)# int f0/1
Router(config-if)# ip nat inside
Router(config-if)# exit
Router(config)# int f0/0
Router(config-if)# ip nat inside
Router(config-if)# ctrl+z

Check on pc
In Command: ping 8.8.8.8 ....... Passs


10) OTHER BRANCH OFFICE

i) HTTP
Ipv4 address: 10.1.1.30
Subnet mask: 255.255.255.0
Default gateway: 10.1.1.1
Dns server: 0.0.0.0

ii) TFTP
Ipv4 address: 10.1.1.20
Subnet mask: 255.255.255.0
Default gateway: 10.1.1.1
Dns server: 0.0.0.0

iii) FTP
Ipv4 address: 10.1.1.10
Subnet mask: 255.255.255.0
Default gateway: 10.1.1.1
Dns server: 0.0.0.0


11) SERVER ROUTER

Router> enable
Router# conf t
Router(config)# hostname r2
Router(config)# int f0/1
Router(config-if)# no shutdown
Router(config-if)# ip address 10.1.1.1 255.255.255.0
Router(config-if)# exit
 
On http
Ping 10.1.1.1 ........ Successful

On tftp
Ping 10.1.1.1 ........ Successful

On ftp
Ping 10.1.1.1 ....... Successful

  
SERVER ROUTER
Router(config)# int f0/1
Router(config-if)# ip nat inside
Router(config-if)# exit
Router(config)# int s0/0/0
Router(config-if)# ip nat outside
Router(config-if)# no shutdown
Router(config-if)# ip address 101.1.1.1 255.255.255.252
Router(config-if)# ctrl+z

check ......
Router# ping 101.1.1.2 ....... successful

Router(config)# access-list 10 permit 10.1.1.0 0.0.0.255
Router(config)# ip nat inside source list 10 interface s0/0/0 overload
Router(config)# ip route 0.0.0.0 0.0.0.0 101.1.1.2
Router(config)# ctrl+z

Check
Router# ping 8.8.8.8 ....... successful
In http
Ping 8.8.8.8
In tftp
Ping 8.8.8.8
In ftp
Ping 8.8.8.8

ROUTER1
Router(config)# int tunnel 1
Router(config-if)# tunnel source ?
Router(config-if)# tunnel source s0/0/0
Router(config-if)# tunnel destination 101.1.1.1 
Router(config-if)#  ip address 172.16.1.1 255.255.255.252
Router(config-if)# ctrl+z
Router# show running-config

SERVER ROUTER
Router(config)# int tunnel 1
Router(config-if)# tunnel source ?
Router(config-if)# tunnel source s0/0/0
Router(config-if)# tunnel destination 100.1.1.1 
Router(config-if)#  ip address 172.16.1.2 255.255.255.252
Router(config-if)# ctrl+z

Router# show running-config
Router# show ip route 

Check .......
R2# ping 172.168.1.1
R1# ping 172.16.1.2

ROUTER1
Router(config)# router ospf 1
Router(config-router)# network  172.16.1.1 0.0.0.0 area 0
Router(config-router)# ctrl+z

SERVER ROUTER
Router(config)# router ospf 1
Router(config-router)# network  10.1.1.0  0.0.0.255 area 0
Router(config-router)# network  172.16.1.2  0.0.0.0 area 0
Router(config-router)# ctrl+z
Router# show ip route ospf

THANK YOU !! 
