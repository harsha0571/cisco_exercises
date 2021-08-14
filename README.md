# CLI commands:
 
## Basic commands 
>en  
config t  
no {command} (to undo that command )  

>shutdown   
no shutdown  

>interface FastEthernet 0/2 or int fa 0/2   
ip address 192.168.10.1 255.255.255.0  
ip route 0.0.0.0 0.0.0.0 192.168.10.1(setting default gateway on router)  
 
>vlan 2  (creates vlan 2)  
vlan 2 name Students  (sets name of vlan 2 to Students)  
vlan database  
 
## Show commands 
>sh span   
show arp  
show run    
show start  
show ip route  (seeing ospf and rip routes)   
sh ip nat translations  
sh int trunk   
sh vlan brief   
sh ip int brief  

 ## Bpdugurad and portfast  
 
>spanning-tree portfast  
spanning-tree vlan 1 priority 0  
spanning-tree bpduguard enable/disable(after disabling shut and no shut to restart)  
 
 ## Per VLAN Spanning Tree (PVST)
>switchport mode trunk (specifies assigning mulitple vlan to same port)  
switchport mode access(specifying that assigning one vlan to one port)  
switchport access vlan 1 (assigning vlan to port with access enabled)  
spanning-tree mode pvst  
 
 ## Static routing 
>ip route {destination network ex: 192.168.10.0}{subnet mask ex: 255.255.255.0}{next hop interface ip}
(mannual  routing for each interface)  
ex: ip route 10.0.1.0 255.255.255.0 10.0.2.1
 
 ## RIP(Routing information protocol )
>router rip  
network 192.168.10.0  

 ## OSPF(Open Shortest Path First)
> router ospf {process_Id}
ex: router ospf 10  
network {network= 192.168.10.0} {wildcard mask = 0.0.0.255} area {area_No}
ex : network 192.168.10.0 0.0.0.255 area 1  


  ## NAT( network address translation)
 
> (config-int) ip nat inside  
(config-int) ip nat outside
    
> For static:  
(config) ip nat inside source static insideIP   outsideIP  
ex : ip nat inside source static 10.0.1.10 203.0.113.3  
    
> For dynamic:
(config) ip nat pool pool_name range of ip's netmask {netmask}
ex: ip nat pool lab 203.0.113.4 203.0.113.14 netmask 255.255.255.240
    
then set access list having range of ip's to be mapped from inside, 
    
>access-list list_no permit {network} {wildcard_mask}
ex: access-list 1 permit 10.0.2.0 0.0.0.255

then,

>ip nat inside source  list list-no pool pool_name
x: ip nat inside source list 1 pool lab
debug ip nat (to see packets live and debug)
     
## Router on a Stick 
First create vlans,
>vlan 2 , vlan 3 , vlan 4 ....
    
then set each vlan to port of switch,
    
>interface range fastEthernet 0/2-3  
switchport mode access  
switchport access vlan 2
   
then set trunk on port connected with router,
    
>switchport trunk encapsulation dot1Q  
switchport mode trunk  
switchport trunk allowed vlan 2,3,4
    
on router,

>int gig 0/0.10   
encapsulation dot1Q vlan  
ex: enc dot1Q 10  
ip add 192.169.10.1 255.255.255.0  


 ## STANDARD ACCESS LIST 
 
Limited flexibility closer to destination rather than source ... 
teacher over student if student is being restricted from accessing teacher network
 
>access-list 10 (upto 99 is standard above is extended list)  
acesss-list list_no deny/permit source destination   
ex : access-list 10 deny 192.168.100.0 0.0.0.255  

then go into appropriate interface and then,

>ip access-group 10 in/out  
access-list 10 permit any ( do remove default global   deny)
(appended to previous deny which will still be high priority)
 
## EXTENDED ACCESS LIST
>access-list 100 permit tcp 192.168.100.0 0.0.0.255 host 192.168.150.101 eq 80
    
then, 

>access-list 100 permit any

## SNMP SERVER CONFIG
>snmp-server community st 
snmp-server community public ro (read only)
snmp-server community private rw (read write)

## NTP SERVER 
>show clock 
ntp server {ip of server providing ntp service}
ex: ntp server 192.168.12.2

## Cisco discovery protocol (cdp)
Layer 2 protocol discovery for cisco devices
>show cdp neighbors detail 

## Link layer discovery protocol (lldp)
Vendor independent link discovery  
First disable cdp, 
> no cdp run  
  lldp run  
  show lldp neighbors detail

## Link aggreation control protocol (lacp)
Aggreation is the combining of several links to  
act as a single connection
> interface range fastEthernet 0/1-2   
  switchport mode trunk   
  channel-group group_no mode active  
  ex: channel-group 1 mode active  

  Only two devices can have common port-channel,
> interface port-channel 1  
  switchport mode trunk  
  show etherchannel summary  
  show etherchannel load-balance  
 

