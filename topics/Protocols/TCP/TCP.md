# Transmission Control Protocol (TCP)

* Layer 4 Protocol : deals with ports  
* As the name , it controls the transmission of segments using different algorithms 
* Stateful : connection is established , connection details are kept in memory of client and server 
* Connection : 3 way handshake 
* Header : 20 bytes (can go upto 60)
* Use case: web connection , db connection , reliable communication


## Connection 

*  Layer 5 property (session)
*  Connection is identified by : source ip-port and destination ip-port which is hashed and mapped to a file descriptor
*  Requires a 3 way handshake to send data 
*  TCP segments are sequenced and ordered 
*  Lost Segments are retransmitted
*  Every connection takes some cpu and memory in both the client and server 

### 3 Way Handshake 

*  A wants to send data to B 
*  A sends SYN request (TCP segment with SYN bit as 1) to B , no data 
*  B sends back SYN/ACK( SYN AND ACK bit as 1) to A
*  A sends ACK(ACK bit as 1) to B , connection is established now 

### Sending data

* After connection is established A sends TCP segment which has data to B 
* B checks the source ip-port , hashes and looks for file descriptor to check if it has connection with A 
* B sends ACK of the data to A
* If A sends 3 segments 1,2,3 then B can only acknowledge the last sequence in this case 3 to inform it has received 1-3 segments
* If in above case B acks with 2 , then A retransmits segment 3 

### Closing connection 

* A wants to close connection , so it sends FIN request(FIN bit as 1) to B
* B acks and sends ACK
* B now sends FIN to A 
* A sends ACK , connection is closed and file descriptor is destroyed 

## TCP Segment 

* 20 bytes header
* Slides into an IP packet as data 
* Ports are 16 bit : Source Port(16 bits) , Destination Port(16 bits)
* Sequence Number (32 bits) : Every time segment is sent sequence no is sent as well 
* Ack number : ack number when ack is sent back 
* Window Size (16 bits) : This means how much data I as a server can handle 
* 9 flags which are FIN , SYN , RST , PSH ,ACK , URG ,  ECE , CWR, NS 

    ![ec71832edb1f2ff1d2ad12da494033ce2b25aafa](https://user-images.githubusercontent.com/29726341/216831462-6b929cc0-c9ba-43a1-b9c5-ee6e7d0cf058.svg)



### Max Segment Size (MSS)

* This means what is the max data than can fit nicely in one TCP segment
* Depends on the MTU of the network 
* Generally 512 bytes but can go upto 1460 
* MTU is 1500 , IP and TCP headers are 20 bytes each so 1500 - 40 = 1460 bytes 

## Flow Control 

* How much data the receiver can handle ? 
* The window that A needs to maintain so B does not get overloaded 
* You can send each segment at a time and then wait for ack , this will increase round trips and increase latency
* So , you send multiple segments , and receiver acks it at once 
* So the question is how much data you can send ? this is called flow control 
* When segments are sent , it is kept in rcvr's buffer and if we keep on sending it will be full and segments can be dropped
* So the solution is to let sender how much to send 
* With each ack from rcvr , it will let the sender know about its window size in bytes , so sender knows how much it can send
* The window size is of rcvr window(16 bit upto 64KB)
* Sliding window : This is the window at the sender side , sender maintains this window to know how much it can send
* Whenever rcvr sends ack of the segment , sender moves the window forward and discards the acks segment(not to retransmit)
* Window Scaling : We can increase the rcvr window by this
* Window scaling factor exchanged only during handshake


## Congestion Control  

* How much the network can handle ?
* So , I want to send max data(segments) at a time without segments getting dropped and thus reducing latency 
* So , routers and boxes in the network through which segments/packets go also have a limit(memory/buffer)
* We dont want to congest the network with data , so we maintain congestion window
* This window is a property of the sender

### Congestion Algorithms 

#### TCP slow start 
* Slow start goes fast : exponentially : so for every segment acks it increases the CWND by 1 MSS
* CWND + 1 MSS after each ACK 

#### Congestion avoidance 

* There is a threshold for slow start
* Once slow starts reaches this threshold , congestion avoidance kicks in 
* CWND is increased for 1(actually by fraction) only on ack of the complete Rount trip
* So you sent 4 segments and only once you rcv acks of the 4 , CWND size will be increased
* Congestion notification : When router buffers fill up they set the ECN bit in IP Packet so sender knows and reduces the CWND

#### Congestion detection

* The moment we get timeout , we know the packets are dropped 
* At that point the slow start threshold is reduced to half of whatever the unacknowledged data is sent 
* The CWND is reset to 1 and slow start starts over again 
* Min threshold is 2 * MSS , can't go below this

    <img width="658" alt="image" src="https://user-images.githubusercontent.com/29726341/216831419-7afcf364-0850-4e3a-b2e2-9be987b48ca7.png">


