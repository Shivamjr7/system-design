# CAP Theorem

* In case of a distributed system , you can either have two of the three : Consistency , Availability and Partition Tolerance
* Consistency : This means if you did  write to your system and then do a read , you should get correct result which you have read
* In case of master -slave replication , you can write to the main and read from slave , and if the slave doesn't have the latest data , it will make your system inconsistent
* Availability : If you do a read/write to your system , it will get you some result(maybe correct/incorrect) but it will get back a result to you
* Partition Tolerance : This means whether the nodes of your system can have network failure between them or not


* In an ideal case all the three would be there for your system
* But guarantying that your nodes will always have communication all the time, or you can withstand partition tolerance is something not true
* Most of the systems today select Partition tolerance as they know there can be network failures between nodes
* And select either Consistency or Availability

## Example 

* Suppose you want to do  write to your system, and you select Consistency
* Then in the above case until write has happened to all the nodes , you will not reply to the user
* Once  write happens you can reply to the user 
* In this case suppose a node fails due to network, you will have to retry and then write 
* Or you can to the user respond that write failed
* In either case your system will be consistent all the time but not available

* Now for the above case if you want Availability
* In that case you can write to the master and reply to the user that write is success
* And in the backend , update all the slave nodes in async way
* If user now tries to read from slave and the sync has not happened it will get old data
* In this case your system will be available all the time, but it will not be consistent
