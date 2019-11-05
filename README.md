# SCRIPT-SPRINT-3

SCRIPTS PACKET TRACER

Sw-01

enable
conf t
ip domain-name grupo2.local
banner motd "Departamento de TI"
username augusto privilege 15 secret batata01
username cleiton privilege 15 secret batata01
username daniel privilege 15 secret batata01
username matheus privilege 15 secret batata01
username yohan privilege 15 secret batata01
line vty 0 15
login local
transport input ssh
exec-timeout 5
exit
service password-encryption
vlan 112
interface vlan 122
ip add 192.168.253.253 255.255.255.0
description VLAN gerenciamento 
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 12,122
exit
interface f0/1
switchport mode access 
switchport access vlan 12
exit
interface f0/2
switchport mode access 
switchport access vlan 12
exit
default-gateway 192.168.22.1
do wr


=============================
Sw-CORE

enable
configure terminal
ip domain-name grupo2.local
banner motd "Departamento de TI"
username augusto privilege 15 secret batata01
username cleiton privilege 15 secret batata01
username daniel privilege 15 secret batata01
username matheus privilege 15 secret batata01
username yohan privilege 15 secret batata01
line vty 0 15
login local
transport input ssh
exec-timeout 5
exit
service password-encryption
vlan 112
interface vlan 112
ip add 192.168.253.254 255.255.255.0
description VLAN gerenciamento
vlan 12 
interface g0/2
switchport mode trunk
switchport trunk allowed vlan 12,122	
no sh
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 12,122	
no sh
exit
interface f0/1 
switchport mode access 
switchport access vlan 12,122
no sh
exit
ip default-gateway 192.168.22.1 
do wr

=========================================
Rt-01

enable
configure terminal
banner motd "Departamento de TI"
username augusto privilege 15 secret batata01
username cleiton privilege 15 secret batata01
username daniel privilege 15 secret batata01
username matheus privilege 15 secret batata01
username yohan privilege 15 secret batata01
ip domain-name grupo2.local
security passwords min-length 8
login block-for 240 attempts 7 within 10
line vty 0 15
login local
transport input ssh
exec-timeout 5
service password-encryption
interface g0/0.12
encapsulation dot1q 12
ip address 192.168.22.1 255.255.255.0
ip helper-addres 192.168.253.5 
description VLAN12
interface g0/0.122
encapsulation dot1q 122
ip address 192.168.253.1 255.255.255.0
ip helper-addres 192.168.253.5 
description VLAN112 Gerenciamento 
exit
interface g0/0
no sh
do wr
