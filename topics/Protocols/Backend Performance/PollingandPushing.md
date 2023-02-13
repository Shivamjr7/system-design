# Polling

* Asking the backend if it has certain information 
* Request - response pattern 
* It is similar to request - response , that is you send a request and backend response
* Only thing is sometimes the backend doesn't have a response

## Short Polling 

* Client can keep on sending request to backend server every x seconds to check if data is available
* By doing this most of the time the server will not have any data, and it will just be an empty request
* Also , the availability of data depends on how frequent you are polling 
* Can cause network congestion as many requests will be sent to the server

## Long Polling 

* Client sends request to the server in an async way
* Server will not respond if data is not available
* It will keep on checking the data and will send it to client once it becomes available
* Less chatty than short polling 
* Apache kafka uses long polling 

## Push pattern

* Client connects to Server
* Server pushes data to the client
* Good for real time info 
* Client should be connected 
* Client may not be able to handle
* Good if not many clients are there
* Rabbit MQ uses push approach
