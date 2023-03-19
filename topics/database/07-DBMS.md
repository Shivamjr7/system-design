# Database System 

* Database : collection of related data 
* Structured and Unstructured data 
* DBMS : to perform operations(insert/delete/update) on the database

## File system vs DBMS 

* Before DBMS 
* OS has inbuilt File system 
* Why we use DBMS : 
  * Client - Server architecture : Data is stored in a central location 
* In File system , if you want to search even 1kb or small data you would need to fetch the complete File where data is stored
* In DBMS, we get data according to the query
* Ease of searching in DBMS 
* Concurrency : DBMS provides whereas FS do not 
* Security : role based access for data in DBMS , not in file system 
* Data redundancy : constraints in DBMS , not in file system 

## 2 tier and 3 tier architecture in DBMS 

### 2 Tier

* Client(library) connects to database (jdbc ...)
* Limited clients 
* Easy Maintenance
* Scalability problem
* Security : clients directly talks to database

### 3 Tier

* Clients connect to application server
* Application server connects to database

### Schema 

* logical representation of database
* Data independence : logical and physical 
* Change in schema and other things (storage change , data migration ) does not affect users

### Keys 

* Keys are attributes(columns) 
* To uniquely identify a tuple in a table 
* Candidate key : 
  * Set of unique keys for a table , it is a minimal set of attributes that can uniquely identify a row.
  * For example for a student , candidate key : {roll no , aadhar no , license no , reg no}
  * We take one of the candidate key as primary key 
* Primary Key : Unique + Not null  , if it is null  2 or more fields can have null values and we cannot differentiate
* Foreign key : one or more attributes that refrences primary key of same or another table 
  * Maintains referential integrity
* Referential Integrity : values should be same for referenced keys 
  * Referenced Table :
    * Insertion : No issues
    * Deletion : may cause issues , as data can be on other table
    * On delete cascade : delete data referenced 
    * On delete null : set data as null(check if foreign key is primary key , if primary key null can cause issue)
    * on delete no action
    * Same for update
  * Referencing Table 
    * Insert : may cause violation 
    * Delete : will not cause violation
    * Updation : may cause violation if foreign key is modified
  * Super Key : Combination of all possible attributes which uniquely identify two tuples in a table
    * Should contain atleast one candidate key

## Relationship model 

### ER Model(Entity- Relationship Model)

* Conceptual /logical view of entities and relationship between them
* Types of attributes
  * Single : one value , eg : roll no , reg no 
  * Multivalued : multiple values , eg : mobile no , address : can have more than one mobile/address
  * Simple : cannot be divided further , eg : age 
  * Composite : can be divided further , eg : name : first name, middle name, last name
  * Stored : fixed value
  * Derived : derived from other attribute , eg : age can be derived from dob
  * key : Unique
  * Non Key 
  * Required : mandatory
  * Optional

* Cardinality : How Entities are connected
  * One to One :  Primary key can be of either side
  * One to Many : Primary key will be of Many side 
  * Many to Many : Primary key will be combination of both primary key of tables


## Normalization

* Technique to remove/reduce redundancy from table
* You can avoid row level duplicay by adding primary key
* For col level if values are repeating there can be some issues :
  * Insertion anomaly
  * Deletion anomaly
  * Update anomaly 
* First Normal Form : Table should not contain any multi valued attribute
* Closure method : to find all possible candidate keys 