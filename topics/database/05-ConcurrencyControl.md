# Exclusive Lock 

* In case of exclusive locks , if I am trying to read or update a value or row/rows , no one else can be connected 
* Means when you try to read/update a value with exclusive lock and anyone else tries to read/update that value it will fail 
* I will be the only one allowed to update that
* There cannot be any shared lock on the same row
* Use case : when you are updating any row/value and do not want others to read stale data 


# Shared Lock 

* When I am reading a value , I want to make sure no change that 
* With shared lock , others cannot update that value / row
* There cannot be any exclusive lock on the same row

* Both the locks are to maintain consistency in the database


