# Database Engines

* Library that takes care of disk storage and CRUD operations 
* Can be a simple key value store
* Can be as complex as supporting ACID transactions
* DBMS can use database engine and build features on top of that (replication , isolation ..)
* Some DBMS give you flexibility to change and in some you cannot change 

## MyISAM

* Stands for Indexed Sequential Access Method
* B Trees point to the row directly (to the offset in heap where value is stored)
* No Transaction support
* Inserts are fast (because you need to write at the end of the file or index)
* Updates and deletes are slow(because when you update , you will have to update the offset for many index which gets changed by update)
* Table level locking(no row level locking)
* MariaDB , MySQL, Percona supports 

## InnoDB

* B+ Tree : index points to primary key which points to a row
* Supports Transactions 
* Row level locking 
* Default for MySQL and MariaDB
* Spatial operations 

## SQLite

* B Tree as index (LSM extension) 
* For local embedded storage of data 
* Postgres like syntax
* Supports ACID 
* Table locking 
* Concurrent reads and writes 
* Web SQL in browser uses it 
* Included in many OS 

## Aria

* Similar to MyISAM

## Berkley DB

* key value embedded database
* Supports ACID
* Used by bitcoin (switched to Level DB)
* Used MemcacheDB

## Level DB

* LSM 
* No Transactions 
* Levels of files : Memtable , level 0 , Level 1-6 

## Rocks DB

* Forked from Level DB
* Transactional 
* Multi Threaded 
