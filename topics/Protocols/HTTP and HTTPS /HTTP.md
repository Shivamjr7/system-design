# Hyper Text Transfer Protocol 

* Request - Response protocol , Layer 7 
* Built on top of TCP (Layer 4)
* Client sends a http request , server replies with http response

## HTTP Request 

* Method : GET , POST , PUT , DELETE 
* PATH : url of the request , there is a limit to how long url can get
* Protocol : HTTP 1.0 , HTTP 1.1 ...
* Headers : content-type : .. , cookie : .. , host:...
* Body : actual request data 
* host header is used because an ip can host multiple websites , to know exactly which folder it came from


## HTTP Response

* Protocol : HTTP 1.0 , HTTP 1.1 ...
* Code : 200 , 404, 501, ..
* Code text : 200 OK , 404 not found . In HTTP 2 code text is not available
* Headers : response headers
* Body : actual response data 

## HTTP 1.0 vs HTTP 1.1 vs HTTP 2

### HTTP 1.0
* In HTTP 1.0 there was a new connection for every request 
* Slow
* Buffering didnt exist
* host header was optional , so multiple website hosting was not possible

### HTTP 1.1.

* Persisted TCP connection : Connection is kept alive to send requests in sequence over the same connection
* Pipelining : You can send multiple requests at once as well , but if first request is not completed , server will block respond with others
* This is because if it sends response 2 first , client will not be able to identify that is was response 2
* So Pipelining is disabled in HTTP 1.1
* Text format for data transfer


## HTTP/2
* Multiplexing : HTTP 2 allows multiple requests to be sent and received in parallel over a single connection, while HTTP 1.1 requires multiple connections to be opened for parallel requests.
* Compression : HTTP 2 uses header compression to reduce the size of request and response headers, while HTTP 1.1 does not have this feature.
* Server Push : HTTP 2 allows servers to push resources to clients proactively, without the need for a separate request.
* Secure by default 
* Binary format for data transfer
* Priortization : HTTP 2 allows clients to specify the priority of different requests, so that the server can prioritize the processing of high-priority requests.
* High CPU usage , because now you have to parse streams to get the requests 
* So in HTTP 1.1 , from browser at a time you can open 6 connections to send 6 http request
* In HTTP 2 you can send multiple requests concurrently over the same connection 
* HTTP 2 can also suffer from TCP Head of line blocking 

    
  <img width="985" alt="image" src="https://user-images.githubusercontent.com/29726341/217308826-88221d0d-a0fa-4d56-a620-39fcd6436f63.png">


## HTTP/3 and QUIC 

* HTTP 3 uses QUIC (built on top of UDP)
* No HOL problems 
* Connection + TLS in one handshake 
* High CPU usage
* Have concept of connection id
* QUIC doesnt allow IP fragmentation, so if MTU is small then you need to repackage UDP into smaller packets


