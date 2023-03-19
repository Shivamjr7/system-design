# Indexes

* Data structure built on top of table so it can analyze the table and give shortcuts to access data on the table
* Like a phonebook index
* If the info is available in the index , it is called inline query
* Some database also keep primary key along with the index you create , so if you create an index on name col and it has id as primary key 
the index will keep name and primary key(id) info as well
* Sequential scan : full table scan 
* Parallel sequential scan : full table scan with multiple worker threads
* Sometimes when you say a query like select * from table where id< 100 and there is an index on id , then it will do index 
scan , followed by heap scan
* Now in the above case if there are million rows in a table and condition is id >100 which is supposed to fetch almost
all rows, db will do a sequential scan as it knows doing index scan followed by sequential scan would cost more
* In cases where you cannot decide if index scan should be done or sequential , a bitmap index scan is done
* Bitmap index scan is also useful when the where clause has two or more index values 
* Bitmap indexing works when cardinality of a data is less , cardinality is the no of unique values present 

# Key vs Non -key column index 

* Non-key index means including a column in index which you often query
* As a result it will only do a index only scan 
* Composite index : means combining two or more keys to form a index
* Order matters in composite index
* If the key you queried is on left side it can do index scan
* If the key you queried is on right side , it will do sequential scan
* Helps when you do queries based on both index of a composite index you created