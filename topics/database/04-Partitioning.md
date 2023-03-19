# Database Partitioning 

* Horizontal : by rows , rows from a particular range are kept as partitions 
* Vertical : partition by columns 
* Types
  * By list : discrete values like states , zip codes 
  * By Range : Dates , ids 
  * By Hash : Hash functions (Consistent Hashing)
* Horizontal Partitioning splits big tables into multiple tables in the same database , the db does it for you
* The split has different names , client is not aware of the partitions and is handled by DB
* Sharding splits database into multiple tables across multiple database servers , client should know the shard to query
* You will have to create and attach partitions 
* set enable partition pruning to on else it will scan on all partitions 

## Pros

* Improves query performance as only a part of DB is queried
* Sequntial scan vs scattered index scan : db makes decision which one to choose better , if you have index but keep on 
going to heap regularily , full scan is better
* Archive old data/partition that are barely accessed

## Cons

* What if you update a row which causes that row to move to a different partition : could be slow
* Inefficient queries scanning all partitions . If your query doesnt know which partition then it can query many partitions
* Schema changes can be challenging 

# Sharding 

## Pros 

* Scalability : Data , Memory
* Security : users can access only certain shards, you can put vip customers in one shard 
* Optimal and smaller index size 

## Cons 

* Client becomes complex as they are aware of the shard 
* Transactions across shards are hard
* Rollbacks are hard
* Schema changes : have to do in all shards 
* Joins : hard to do joins , better to do partitioning 
* You should know the shard key 