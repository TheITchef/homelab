# Cisco WS-C3560CG-8PC-S — Running Config

> Status: Reset — pending baseline config  
> Serial: FOC1820Y6HW  
> IOS: 12.2(55)EX2 ipbase


Current configuration : 2758 bytes
!
version 12.2
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec localtime
service password-encryption
!
hostname itc-uvy-sw-01
!
boot-start-marker
boot-end-marker
!
enable secret 5 $1$RHu6$P54iXsZH95iNPv5loc4oS0
!
username admin privilege 15 secret 5 $1$zNka$GKz6XAEjIKtLifxghangi/
!
!
no aaa new-model
clock timezone CET 1
clock summer-time CEST recurring last Sun Mar 2:00 last Sun Oct 3:00
system mtu routing 1500
!
!
no ip domain-lookup
ip domain-name ad.theitchef.com
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
!
!
!
vlan internal allocation policy ascending
!
ip ssh time-out 60
ip ssh version 2
!
!
interface GigabitEthernet0/1
 description esxi-01
 switchport access vlan 30
 switchport trunk encapsulation dot1q
 switchport mode access
 spanning-tree portfast
!
interface GigabitEthernet0/2
 description esxi-02
 switchport access vlan 30
 switchport mode access
 spanning-tree portfast
!
interface GigabitEthernet0/3
 description mgmt-01
 switchport access vlan 30
 switchport mode access
 spanning-tree portfast
!
interface GigabitEthernet0/4
 description DC01
 switchport access vlan 20
 switchport mode access
!
interface GigabitEthernet0/5
 description PAW-T470s
 switchport access vlan 20
 switchport mode access
 spanning-tree portfast
!
interface GigabitEthernet0/6
!
interface GigabitEthernet0/7
!
interface GigabitEthernet0/8
!
interface GigabitEthernet0/9
!
interface GigabitEthernet0/10
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 999
 switchport mode trunk
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan10
 description MGMT
 ip address 10.0.10.11 255.255.255.0
!
ip default-gateway 10.0.10.1
ip classless
no ip http server
no ip http secure-server
!
ip sla enable reaction-alerts
!
!
banner motd ^C***********************************************
*                                             *
*          theITchef HomeLab                  *
*                                             *
*    itc-uvy-sw-01 // Cisco 3560-CG          *
*    L3 Core Switch // Access Layer          *
*                                             *
*  UNAUTHORIZED ACCESS IS PROHIBITED         *
*  All sessions are logged and monitored     *
*                                             *
*  Authorized users only                     *
*  ad.theitchef.com                          *
*                                             *
***********************************************
^C
!
line con 0
 exec-timeout 15 0
 logging synchronous
line vty 0 4
 access-class MGMT-ACCESS in
 exec-timeout 15 0
 login local
 transport input ssh
line vty 5 15
 access-class MGMT-ACCESS in
 exec-timeout 15 0
 login local
 transport input ssh
!
ntp server 10.0.10.1
end
