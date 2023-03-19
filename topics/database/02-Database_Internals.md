# Database Internals

## How Tables and indexes are stored on disk 

## Rows and Pages 

* Row : in mysql , oracle row_id is same as primary key , in postgres has its own row_id
* Page : Fixed size memory location on the disk where rows are stored
* When you want to get a row , you will have to get the page where the rows are stored
* Once you get that page , you will get all rows and not a particular data
* Then db would have to parse and get the record based on your filter
* Each page has a size( 8 KB in Postgres and 16KB in MySQL)


## IO

* IO operation is a read request to the disk 
* We try to minimize this as much as possible
* An IO can fetch one or more page depending on disk partitions 
* Some IOs go to the OS cache and not to disk 

## HEAP

* Data structure where table is stored with all its pages 
* This is where actual data is stored 
* Traversing heap is expensive as it has lot of data 
* This is why we need indexes to tell which part of heap to read

## Index

* Data structure that has pointers to the heap (B tree or LSM trees)
* Used to quickly search for something 
* You can index or more column 
* Index tells you which page you want from the heap 
* The smaller the index , the more it can fit in memory , faster the search 
* It will store the value and the page no 

## Row vs column based database

* In Row based each row with all values are stored in this type of DB . So when we query , it will fetch a block from the heap. Each block fetch is a IO operation. 
* The chance is may be we get the value , if not fetch the next block and then we get the complete row value once we find 
* each column value is stored in this type of DB . if we do select * from in column db where column_field_=value , it will first fetch that column (1 block) and then it will have to fetch each block for each value of the row corresponding to that.
* Not useful for writing as IO operations would be much
* Column based is great if you do aggregate function on a single column 

## Primary Key vs Secondary Key

* In case of Primary key , data is organized in pages around this key
* If it is sequential then data will be organized in way so it sequential according to primary key
* It is also called clustered index or IOT in oracle
* Helpful for range queries
* In case of secondary key , data is organized randomly but the index is organized , but you still need to go to heap to fetch the data 

