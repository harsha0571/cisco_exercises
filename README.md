### cli commands:
 en  
 config t  
 interface FastEthernet 0/2  
 shutdown  
 no shutdown  
 ip address 192.168.10.1 255.255.255.0  
 ip route 0.0.0.0 0.0.0.0 192.168.10.1(setting default gateway on router)  
 ip route <destination network ex: 192.168.10.0><subnet mask><next hop interface> (mannual  routing for each interface)  
 no <command to remove fromt mannual route>  
 spanning-tree portfast  
 spanning-tree vlan 1 priority 0  
 spanning-tree bpduguard enable/disable(after disabling shut and no shut to restart)  
 switchport mode trunk (specifies assigning mulitple vlan to same port)  
 switchport mode access(specifying that assigning one vlan to one port)  
 switchport access vlan 1 (assigning vlan to port with access enabled)  
 spanning-tree mode pvst  
 sh span   
 show arp  
 show run    
 show start  
 show ip route  
 vlan 2  
 exit  
 vlan database  
 vlan 2 name Vlan2  
 
 ## router rip  
 network 192.168.10.0  

 ## router ospf <process_Id>  
    ex: router ospf 10  
 ## network <network= 192.168.10.0> <wildcard mask = 0.0.0.255> area <area_No>  
    ex : network 192.168.10.0 0.0.0.255 area 1  
