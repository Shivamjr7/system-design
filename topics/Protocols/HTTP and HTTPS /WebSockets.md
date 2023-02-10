# WebSockets

* Bidirectional Protocol : Client and Server can exchange data 
* We have TCP as bidirectional in layer 4 but just exposing it in layer 7 is bad idea
* It is over HTTP , so it is firewall friendly , port 80 and 443 is always allowed by everyone
* To switch to websocket over HTTP , an upgrade header is sent 
* The Server then replies with 101 response saying it is now switching protocols 

## Use cases

* Chatting application 
* Live feed 
* Multiplayer gaming 
* Show client progress/logging

## Cons
* Proxying is tricky
* L7 LB challenge (timeout)
* Stateful , difficult to horizontally scale 
* Better to use Long Polling or SSE sometimes