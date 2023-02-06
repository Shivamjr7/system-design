# MSS vs MTU

## MTU 
* How large the packet can get ?
* MTU is the max size of frame 
* Size of the frame determines the size of the segment 
* The more data you can send in a single segment the better because it would decrease latency 
* MTU is the property of network , default : 1500 bytes 
* If your IP packet has a size > MTU , it will be fragmented

## MSS

* Determined based on MTU 
* MSS = MTU - IP headers - TCP headers 

    <img width="658" alt="image" src="https://user-images.githubusercontent.com/29726341/216868128-b7e05416-0588-46a5-adf3-e8daa4066d08.png">

## Path MTU discovery 

* Since MTU is a network interface property , each host can have different MTU 
* Path MTU will determine the MTU of the complete network path
* It needs to be the smallest MTU of the host in the network path
* Client sends IP Packet with DF flag , so in case a smaller MTU is encountered , it says not to fragment but to tell back the client
* In case a smaller MTU is encountered , a ICMP message is sent back to client(Fragmentation needed)

