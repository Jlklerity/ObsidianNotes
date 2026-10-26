

## Reader threads only read object
## Writer threads modify object
## Writers must have exclusive access to the object
## Unlimited number of readers can access the object


# Occurs frequently in real system e.g. online airline reservation systems, multithreaded caching Web proxy


## Solution

```c
semaphore rw mutex = 1;
//for the writers. 
semaphore mutex = 1;
//for read_count
int read_count = 0; 

//writers 
while (true) 
{
 wait(rw_mutex); 
 . . . 
 /* writing is performed */
  . . . 
  signal(rw_mutex); 
}

//readers 
while (true) 
{ 
 wait(mutex); 
 read_count++; 
 if (read_count == 1) 
	  wait(rw_mutex); 
 signal(mutex); 
 . . . 
 /* reading is performed */
 . . . 
 wait(mutex); 
 read_count--; 
 if (read_count == 0) 
	 signal(rw_mutex); 
 signal(mutex);
}
```
