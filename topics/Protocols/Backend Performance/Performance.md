# Nagel's Algorithm 

* Some time the client wont send data to the server and wait for MSS to fill
* This is Nagle's Alogrithm
* In the above case if there is very small data in your TCP segment , it will not be sent to server
* This will increase the latency and will be very hard to debug
* Note : It will not send data in the below case :
* When there is ack waiting and data has not filled the MSS 
* In case there is no ack waiting , it will send no matter what
* You can disable Nagle's Algorithm using TCP_NODELAY to TRUE/ON


# Disabled Acknowledgement

* Sometimes the server thinks it is waste to ack the segment right away
* So it decides to ack all the segments together
* In this case the client since has not rcvd ack will think if the packet was dropped and retransmit
* Can also cause timeout in client side waiting for ack 
* Performance degradation
* If both Nagle's and Delayed ack is enabled it can lead upto 400ms delay
* Each party will end up waiting for each other
* Disabling dealyed ACK : TCP_QUICKACK option

# Cost of Connections 

* Most implementations uses connection pooling to enhance performance
* Eager vs Lazy loading 
* Eager loading : most servers do a warmup , so that slow start kicks in and connections are warm and fast
* Lazy loading : In this case the first requests will be slow , since the TCP slow start algo will just start and window will be small


# TCP Fast Open 

* With TCP Fast Open we can send data during the TCP handshake
* Client and Server establishes connection , server sends an ecncrypted cookie to client
* Next time when the client connects to the same server , it sends TFO cookie in TCP Options during handshake
* Server authenticates the cookie and sends Response + SYN/ACK

# TCP Head of line blocking (HOL)

* TCP orders the packets in the order they are sent
* So if you send 4 packets , and 1 does not arrive you will no get ack of remaining 3 until 1 arrives or is retransmitted
* HTTP uses same connection to send multiple requests
* So if 2 requests each of which has 2 segments are sent Req 1(1,2) , Req2(3,4)
* If 2,3,4 are rcvd but 1 is not , it will block request 2 as well which is part of segment 3 and 4 unitl segment 1 is retransmitted 
* This is Head of Line blocking 