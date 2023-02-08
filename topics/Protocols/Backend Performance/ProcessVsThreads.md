# Backend Execution Patterns

## Process vs Thread

### What is a Process ?

* Process is a set of instructions 
* Has an isolated memory 
* Has a id , PID 
* scheduled in the CPU 
* Each process is scheduled in the CPU by the scheduler

### Threads

* Light weight Process
* Set of instructions as well
* Shares memory with Parent process 
* Also has a ID , thread-id
* Scheduled in the CPU 


* In case of a Application or Process with Single Thread , all the instructions will be executed by a single CPU , example : Node JS  
* Application can have multiple process , each process can have its own memory
* In this case multiple process will be scheduled in multiple CPU/cores
* Process apart from their memory also share a memory called buffered or shared memory pool

* In multi threaded , one process can have multiple threads
* Shared memory
* Can take advantage of multiple cores 
* Race condition
* Can take less memory 
* Locks and Latches 

## Context Switching 
* The CPU knows when to temporarily suspend a process and switch to another process because of the operating system's scheduler.
* The scheduler is a component of the operating system that determines which process should be running on the CPU at any given time.
* When a process requests to read from memory or I/O, it generates an interrupt, which is a signal that is sent to the CPU to indicate that an event has occurred that requires attention
* The CPU handles the interrupt, suspends the execution of the process, and switches to the scheduler, which selects another process to run
* When the memory or I/O operation has completed, the CPU receives another interrupt, and the process that was suspended is resumed and continues its execution.
* The CPU uses this mechanism of context switching and interrupt handling to efficiently manage the execution of multiple processes and to ensure that each process gets a fair share of CPU time.