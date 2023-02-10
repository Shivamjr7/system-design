# Remote Procedure Call (RPC)

* When 2 or more service communicate with each other , request - response design is followed
* Generally services expose HTTP endpoints which other service can call and get result
* Services generally use REST to communicate with each other and json as the way to exchange data 
* Each service is implemented in a language of choice and has http library in that language to make the call and get response
* So , when a service is unavailable you also need to handle errors , retries and many other things 
* Also the same needs to be done for all services which are calling a particular service 
* For example : For a notification service which sends OTP to your email , it can be called by many services and all services need to write the same logic of calling , handling errors , retries etc..

* In RPC , services communicate with each other as they are calling a normal function
* With RPC , you abstract out the repetitive tasks like communication protocol , object creation , failures , retries  and just focus on writing business logic
* Also you dont have to serialize your request in json format and then at the Server end deserialize json to Object 
* With gRPC you get protocol buffer which is way faster than json.
* RPC looks like a function call but happens over the network 

## Stubs 

* The request from service 1 needs to be converted to a format which service 2 can understand and the response needs to be converted to a format which service 1 can understand
* Stub does the above work 
* It converts the methods, request type in a form which can be used by the service
* So if two services are communicating with each other both generates a stub
* Service1 will talk to the stub and then the stub will send data to Service 2
* Service 2 stub takes the data and understands it and then calls the method on Service 1
* This allows us to write our services in any language and then generate stub so any two services can talk to each other

## How to generate Stubs 

* There will be a interface definition language (.proto in gRPC) in which both request and response type will be defined
* Services will make use of this .proto file and generate Stubs in their language of choice

## Communication 

* RPC can use any layer 4 protcol : TCP or UDP 
* gRPC by default has HTTP/2 which has many advantages like multiplexing , compression , streaming, connection pool  

## Cons 
* Stub needs to be regenerated for every change in signature 
* Testing RPC is quite complex
* Browser support is limited
