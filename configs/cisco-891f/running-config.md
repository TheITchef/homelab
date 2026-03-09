# Cisco C891F-K9 — Running Config

> Status: Reset — pending baseline config  
> Serial: FCZ2213E0EW  
> IOS: 15.4(3)M3 advipservices

Building configuration...

Current configuration : 4639 bytes
!
! Last configuration change at 21:00:57 CEST Mon Mar 9 2026
!
version 15.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname itc-uvy-rtr-01
!
boot-start-marker
boot-end-marker
!
!
enable secret 5 $1$Lld0$WJateNMK/zK2uDO6bXBKv.
!
no aaa new-model
clock timezone CET 1 0
clock summer-time CEST recurring
!
!
!
!
!
!
!
!
!
!


!
ip dhcp excluded-address 10.0.10.1 10.0.10.20
ip dhcp excluded-address 10.0.20.1 10.0.20.20
ip dhcp excluded-address 10.0.30.1 10.0.30.20
ip dhcp excluded-address 10.0.99.1 10.0.99.20
!
ip dhcp pool MGMT
 network 10.0.10.0 255.255.255.0
 default-router 10.0.10.1
 dns-server 10.0.20.2
!
ip dhcp pool LAN
 network 10.0.20.0 255.255.255.0
 default-router 10.0.20.1
 dns-server 10.0.20.2
!
ip dhcp pool SERVERS
 network 10.0.30.0 255.255.255.0
 default-router 10.0.30.1
 dns-server 10.0.20.2
!
ip dhcp pool WIFI
 network 10.0.99.0 255.255.255.0
 default-router 10.0.99.1
 dns-server 10.0.20.2
!
!
!
no ip domain lookup
ip domain name ad.theitchef.com
ip cef
no ipv6 cef
!
!
!
!
!
multilink bundle-name authenticated
!
!
!
!
!
!
!
!
cts logging verbose
license udi pid C891F-K9 sn FCZ2213E0EW
!
!
username admin privilege 15 secret 5 $1$RwQQ$etEQeMmXaFTTQ4iCjLt3s/
!
!
!
!
!
ip ssh time-out 60
ip ssh version 2
!
!
!
!
!
!
!
!
!
!
!
interface BRI0
 no ip address
 encapsulation hdlc
 shutdown
 isdn termination multidrop
!
interface FastEthernet0
 no ip address
 shutdown
 duplex auto
 speed auto
!
interface GigabitEthernet0
 description TRUNK-TO-3560CG
 switchport trunk native vlan 999
 switchport mode trunk
 no ip address
!
interface GigabitEthernet1
 no ip address
!
interface GigabitEthernet2
 no ip address
!
interface GigabitEthernet3
 no ip address
!
interface GigabitEthernet4
 no ip address
!
interface GigabitEthernet5
 no ip address
!
interface GigabitEthernet6
 no ip address
!
interface GigabitEthernet7
 no ip address
!
interface GigabitEthernet8
 description WAN-ISP
 ip address dhcp
 ip access-group WAN-IN in
 ip nat outside
 ip virtual-reassembly in
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
!
interface Vlan10
 description MGMT
 ip address 10.0.10.1 255.255.255.0
 ip helper-address 10.0.20.2
!
interface Vlan20
 description LAN
 ip address 10.0.20.1 255.255.255.0
 ip helper-address 10.0.20.2
 ip nat inside
 ip virtual-reassembly in
!
interface Vlan30
 description SERVERS
 ip address 10.0.30.1 255.255.255.0
 ip helper-address 10.0.20.2
 ip nat inside
 ip virtual-reassembly in
!
interface Vlan40
 description STORAGE
 ip address 10.0.40.1 255.255.255.0
 ip helper-address 10.0.20.2
 ip nat inside
 ip virtual-reassembly in
!
interface Vlan50
 description DMZ
 ip address 10.0.50.1 255.255.255.0
!
interface Vlan99
 description WIFI
 ip address 10.0.99.1 255.255.255.0
 ip helper-address 10.0.20.2
!
interface Async3
 no ip address
 encapsulation slip
!
ip forward-protocol nd
no ip http server
no ip http secure-server
!
!
ip nat inside source list 1 interface GigabitEthernet8 overload
ip route 0.0.0.0 0.0.0.0 GigabitEthernet8 dhcp
!
ip access-list extended MGMT-ACCESS
 permit tcp 10.0.10.0 0.0.0.255 any eq 22
 permit tcp 10.0.20.0 0.0.0.255 any eq 22
 deny   tcp any any eq 22 log
ip access-list extended WAN-IN
 deny   ip 10.0.0.0 0.0.255.255 any log
 deny   ip 172.16.0.0 0.15.255.255 any log
 deny   ip 192.168.0.0 0.0.255.255 any log
 permit ip any any
!
!
access-list 1 permit 10.0.0.0 0.0.255.255
!
control-plane
!
!
mgcp behavior rsip-range tgcp-only
mgcp behavior comedia-role none
mgcp behavior comedia-check-media-src disable
mgcp behavior comedia-sdp-force disable
!
mgcp profile default
!
!
!
!
!
!
banner motd ^C***********************************************
*                                             *
*          theITchef HomeLab                  *
*                                             *
*    itc-uvy-rtr-01 // Cisco 891F            *
*    Edge Router // WAN/ISP                  *
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
 no modem enable
line aux 0
line 3
 modem InOut
 speed 115200
 flowcontrol hardware
line vty 0 4
 access-class MGMT-ACCESS in
 exec-timeout 15 0
 login local
 transport input ssh
!
scheduler allocate 20000 1000
ntp server 216.239.35.0
!
!
!
end

