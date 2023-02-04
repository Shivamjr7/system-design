
# Domain Name System (DNS)

* You cant remember all the IPs , also IP of a server can change , so you have a text or address and DNS query gives you IP
* It can give you 1 IP or multiple IPs
* You can do client side load balancing based on this info(multiple IPs)
* It can also provide you other info like what is your mail server ? what port i can connect to ....
* geo DNS : can give you IP of the closest server : reducing latency
* Built on top of UDP , port 53 (this can be any port though)
* Many records
    * A : A protocol gives you IP
    * CNAME : gives you alias
* How DNS works ?
    * When you connect to any network , it gives you a default DNS resolver(generally your router, but you can overwrite)
    * DNS resolver is hardcoded and you already know what is your DNS resolver IP
    * You send a UDP packet to Resolver asking what is the IP address of say www.google.com
    * Resolver asks the ROOT server to give the server which knows about Top level domain (.com)
    * Root replies with a TLD server IP and now Resolver connects to the TLD
    * Resolver asks TLD server to now give the ANS for www.google.com
    * TLD replies with ANS and now Resolver asks ANS : what is the IP of www.google.com ?
    * ANS replies with IP or multiple IPs and now Resolver gives you back the IP
    * Now you connect to the IP or any one IP of multiple IPS using TCP or UDP
    * In the above case also the Resolver can cache the IP and provide you next time you query

      ![DNS QUERY DECONSTRUCTED.png](..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2F_9%2F3_5ykpr111n0qj7cxcjmjdqh0000gn%2FT%2Fcom.apple.Notes%2FHardLinkURLTemp%2FCFC6307C-0820-4D8F-AE0F-75D708119470%2F1665585202%2FDNS%20QUERY%20DECONSTRUCTED.png)

* Why so many trips to get IP ?
    * This is because you should always search in smaller datasets and so data is partitoned over multiple servers(ROOT , TLD, ANS)

* How Resolver knows which response belongs to which request in case of multiple requests ?
    * There is a Transaction ID header in DNS(UDP) which helps for mapping request-response

* DNS is not encrypted : so your ISP knows all the domains you visit
* To solve this there is DNS over TLS (DoT) and DNS over HTTPS(DoH) : port 443
* DoH means you will send DNS query like a HTTP request
* Many prefer DoT
* Many Attacks : DNS Hijacking , DNS cache posioning
* nslookup to demo DNS (example : nslookup www.google.com)


Amazone Route 53 : https://intellipaat.com/blog/what-is-aws-route53/