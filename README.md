# strave-free-readers-writers-problem

the readers-writers prblem is a classical problem of synchronization in the field of computer science. It is concerned with the writers and readers accesssing the critical sections of their code. The critical section of their code refes to that part of the code which has the usage of some resources which are used both during the writing and reading pocesses which makes the synchronized access to these resources essential for the proper functioning of the overall process. 

firstly I would like to present the classical solution (not starve free) which would be followed by the starve free solution to the problem.

## data structures involved -->

We'll be using semaphores which can be used to track the allocation/deallocation of resources, the waiting process requests, available instances of a resource etc. We have some kind of a queue associated with each semaphore to keep track of the waiting processes and provide them with resources whenever it finds them free. 

### semaphores:
```cpp
// semaphores involed-->
        
        semaphore rw_mutex = 1;   // intialized to 1
        // used to ensure mutual exclusion between the readers and writer processes
        
        semaphore mutex = 1;      // initialize to 1
        // it is used to ensure mutual exclusion while the variable read_count gets updated
        
        int read_count = 0;       // initialize to 0
        // its signifies the number of readers currently reading the subject 
```

### writer process:

