# strave-free-readers-writers-problem

the readers-writers prblem is a classical problem of synchronization in the field of computer science. It is concerned with the writers and readers accesssing the critical sections of their code. The critical section of their code refes to that part of the code which has the usage of some resources which are used both during the writing and reading pocesses which makes the synchronized access to these resources essential for the proper functioning of the overall process. 

firstly I would like to present the classical solution (not starve free) which would be followed by the starve free solution to the problem.

## data structures involved ->

We'll be using semaphores which can be used to track the allocation/deallocation of resources, the waiting process requests, available instances of a resource etc. We have some kind of a queue associated with each semaphore to keep track of the waiting processes and provide them with resources whenever it finds them free. 

Here is a classical solution to the readers-writers problem where the readers have a priority i.e. no reader should wait for other readers to finish simply because a writer is waiting: 

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
```cpp
// writer process
    do {
        wait (rw_mutex); 
        // wait for the semaphore rw_mutex to be available

        /*   perform writing   */

        signal(rw_mutex);
        // signal that a writer or a reader may resume its action

    } while (true);
```

### reader process:
```cpp
        do{
        wait (mutex);
        // wait for read_count to be updated
        
        read_count++;
        // increment read_count
        
        if(read_count==1) wait(rw_mutex);
        // if the reader is the first one, it needs to acquire rw_mutex to start reading 
        
        signal(mutex);
        
        /*   reading performed   */
        
        wait(mutex);
        
        read_count--;

        if(read_count==0) signal(rw_mutex);
        // if no reader is reading, a writer may get a chance
        
        signal(mutex);

    }while(true);
```

The problem with this approach is that the writers may starve here as the priority rests with the reader and as long as any reader is present, a writer may have to wait for a very long time to be able to write.

#starve free approach-->

















