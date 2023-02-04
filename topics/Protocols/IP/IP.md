# Internet Protocol :


## IP Address  :

* Layer 3 Property , generally assigned by ISP or router
* Network and Host Portion : a.b.c.d/x , first 24 bits are network, rest 8 bits are host

## Subnet Mask : 

* The subnet has a mask 255.255.255.0
* Used to determine if a IP address is in same subnet or network 
* If you are sending a packet to another IP address and it is in same subnet , you can use MAC address to send it 
* If not in same subnet , it will need to be routed via router to the destined network
* If you have a database you should keep it in the same subnet or network so communication happens through a switch 


## ICMP : Internet Control Message Protocol 

* Designed for Informational messages (Host unreachable , Fragmentation needed , Packet expired)
* IP level Protocol  : Layer 3 info only needed 
* Some routers can block due to flooding attacks 
* TTL determines the no of hops it can take 
* Ping and Traceroute uses this 

## IP Packet 


* Has header (20 bytes) , can go upto 60 bytes if options are enabled 
* Data section : 65536  : Data portion is TCP / UDP 
* MTU or Maximum Transmission Unit : Max size of a frame  that can be sent without fragmentation : 1500 bytes 
* Version : 16 bits : IPV4 or IPv6
* IHL : header length , determine the size of headers in IP Packet 
* Total length : 16 bit data + header 
* TTL : Max hops that an IP packet can do before it is dropped , if there is no TTL an IP packet can go on idenfinetly in come cases.
* Protocol : Protocol of data inside IP packet (TCP/UDP/...), routers can check this and decide if it wants to read that data or not 
* Source and Dest IP : 4 bytes each 
* Options : if IHL > 5  
* ECN  (Explicit Congestion Notification): This bit is set by the router.
    * There will be many IP Packets coming to the router and it has some memory or buffer to store them , parse them and then route
    * If the buffer starts to fill , router will set this bit to control congestion.
    * If the buffer is full, router can drop packets but the bit will be set 


![ip_header](https://user-images.githubusercontent.com/29726341/216752822-39f55401-ef17-438e-949a-03febf45f5d6.svg)


## ARP : Address Resolution Protocol 

* To find out MAC address from IP address 
* ARP Table is cached IP -> MAC mapping 
* Client wants to send data to an IP but dont know the MAC address
* Client will check if the IP is in same subnet , then broadcasts an ARP request to the network
* If not in same subnet , router will send broadcast message in the dest IP network
* Client caches the MAC then in the ARP Table
* What if someone fakes and says replies with others MAC address (ARP poisoning): packets will go to the attacker

