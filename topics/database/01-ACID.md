# Transaction
* Set of queries
* 1 unit of work 
* Starts with BEGIN 

## Lifespan
* BEGIN
* COMMIT
* ROLLBACK
* Crash(Unexpected crash) - ROLLBACK

# Atomicity

* All queries in a transaction must succeed
* If one query fails, txn should be rolled back
* Some database on writing , writes to disk while some writes to memory and then when you say commit , writes to disk
* In case of database crash, db should roll back the queries which were written as a part of txn 

# Isolation

* Isolation is the result of running one txn in complete isolation from another concurrent txn. As a result we get read phenomena
* There can be multiple tcp connections to the database . We want to know if the query run by us is able to see may be the change run by another query? Does it see the change ? Depends on the database design

## Dirty Reads

* When we change by some other concurrent txn which has not been committed yet 
* Chances are the txn will get rolled back, and we would have read the  changes done by the txn

## Non - repeatable reads

* You are doing some txn 
* Now another txn comes and changes values of row and commits
* Now when you read the values again in the same txn through some aggregate function you get the latest result
* In MYSQL or SQlServer , when there is a change by txn it changes in the same row but in Postgres it creates a new version of row and changes value


## Phantom reads

* Happens when you have a range query and some rows are inserted after you have read
* TXN1 : reads the table 
* TXN2 : inserts a new row in the table which changes the result 
* This is called phantom read because now a new row was inserted 

## Lost Updates 

* If I have changed a row and some other txn updates the same row , I will get inconsistent result. This can be solved by locking the row


## Isolation levels 

* Read uncommitted : No isolation , any change from the outside is visible to the txn , committed or not(No DB except SQL server supports this) . This means you can read uncommitted values and hence you can get dirty reads in this case
* Read committed : Every query in txn sees only committed changes by other txn , can be good or bad for particular use cases
* Repeatable read : This means that when the query reads a row , that row will remain unchanged while it is running , no matter how many times I read the row during txn
* Snapshot :   Each query in the txn sees the changes that have been committed up to the start of the transaction. It is like snapshot version of database at the moment . This guarantees to get rid of every read phenomena
* Serializable : txn are run as if they are serialized one after the other. This is slow

* Each DBMS implements isolation level differently.
* Pessimistic : lock row , table , pages whichever is changed to avoid lost updates
* Optimistic : No locks 
* Repeatable read : locks the row , could be expensive if you read a lot of rows , In postgres this is similar to snapshot 
* Serializable are usually implemented with optimistic concurrency control


# Consistency

## Consistency in data 

* State of the data that is currently persisted 
* Is it consistent with the data model 
* Defined by the user : who builds the data model 
* Referential integrity: data linking to another data in table 
* Atomicity 
* Isolation


## Consistency in reads

* Your data might be consistent in disk but reading might be inconsistent due to data in multiple instances
* And those multiple instances might slightly be out of sync 
* Happens when something is written to master, but then you read it immediately from slave which has not yet synced to master


# Durability

* Anything that we write is stored or committed to the database
* If the database crash after I write the change and when it gets back , the change will be there 
* So If say commit and then switch off power the data better be there
* Durability slows down system because writing to disk is slow
* Sometimes when we commit , db says commit success and writes to OS Cache
* In case of OS crash , your data will be lost 
* fsync command is used to skip writing data to OS cache and write directly to disk
* WAL : write ahead log: write changes to file and then we write to memory
* Async snapshot