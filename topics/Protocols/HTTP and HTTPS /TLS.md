# HTTPS / TLS (Transport Layer Security)


* In HTTP data sent in plain text , so any one in the middle can see your data , you need to encrypt it
* Layer 5 (session)
* Anything below layer 7 can be encrypted
* You can encrypt your data with a key(a large prime number)
* Symmetric key : client and server both use same key for encrypting and decrypting
* Asymmetric key : different key for encryption and decryption , more cpu and time 
* So this key needs to be exchanged between the client and server
* But how would you exchange the key without someone in the middle not catching the key
* There will be 2 algorithms : 1.Key exchange 2.Encryption(for data) 

## TLS 1.2
* 2 round trips
* Client sends a client hello and says let's use this key exchange algo to the server
* Server sends the public key along with the certificate(so client knows it is actually server)
* Client generates a symmetric key and encrypts it with Server's public key and sends fin to the server
* Server decrypts the data sent using its private key and gets the symmetric key now
* Data can be exchanged now in a secure way 

## TLS 1.3 
* Uses a better key exchange algorithm
* Client and Server both will have private key each with them x and y lets suppose
* Client will combine x with public key (g^x)% n and send to server, will also send public key
* Server now takes the data sent and combines with private key y to get the symmetric key (g^xy) % n
* Server also combines public key with its private key(y) and sends it to client(g^y)%n
* Client rcvs the data and combines with its private key to get symmetric key(g^xy)%n
* 1 round trip , can be 0 as well in case a client already connected with server before(will use symmetric key generated earlier)

