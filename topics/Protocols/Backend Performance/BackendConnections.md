
# How Backend accepts connections 

* Your computer has multiple NIC : ethernet-adapter , wifi adapter
* Each has its own IP
* Your listener always listens on IP:Port
* Your process should not listen on all interfaces , but on a specific interface(IP:Port), loopback : 127.0.01
* When the client connects , kernel does the actual 3 way handshake
* Socket is what we listened on , connection is the output , socket can have many connections

## Connection Establishment
* Kernel creates a socket(based on interface you are listening ) and two queues Syn and Accept
* Client sends a syn request
* Kernel adds syn to syn queue, replies with syn/ack
* Client replies with ack
* Kernel matches the ack to the syn to find the corresponding client which acked
* Kernel removes the connection and places it in accept queue , a file descriptor is created for the connection
* When the backend calls accept() method , connection is removed from accept queue and passed to backend process


## Problems which can happen with backend connection

* Backend is lazy and not acception connections fast enough 
* In this case , syn will not be placed as accept queue is full and connection establishment takes more time
* Client can do Syn flood attack 
* Small backlog(size of syn queue )

## Send and Receive buffers

* Kernel also creates send and rcv buffers
* When client sends data it specifies the file descriptor 
* Kernel takes the data and puts it in rcv buffer
* When the backend process calls read() , data is copied from the rcv buffer to backend process memory
* Similarly , when the backend wants to write data to the client it writes in the send buffer and kernel sends it to client
* Zero copy : In this data is put between kernel and user shared space/memory and backend app doesnt need to copy the data 
* epoll and iouring : in async way , you ask kernel to let you know when the data is available in rcv buffer and then you can copy