# How to do Capacity Estimation 

* It doesn't have to be exact but approximate
* Why do you need to do this ? : for availabilty , no of transactions , amount of data to be stored 
* example : there are 17k connections per day , you would want to know TPS
  * Instead of 17k/84600 -> 20k/100000
* Try to Know Power of 2's till 1024 : 2,4,8,16,32,64,128,256,512,1024
* Calculate in Millions instead of lakhs 
* Storage capacity : 
  * 1 byte = 8 bits
  * 1 Kb =  1024 bytes 
* 1 million transaction per day = 12 TPS , 700TPM , 42000 TPH
* Round of to the power of 10's and 2's
* Latency no every programmer should know 
