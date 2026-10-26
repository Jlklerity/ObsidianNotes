


## Performs an atomic exchange on a [[shared lock variable]] in memory.

## Before entering into a critical section, a process inquires about the lock.

## If it is locked, the process waits till it becomes unlocked and takes the lock to execute in the critical section.

## TSL is put simply a single atomic hardware instruction. [[Atomics]]

## Pro: Satisfying mutual-exclusion
## Con: Does not satisfy [[bounded-waiting]]

```c
boolean TestAndSet(boolean* target) //atomic operation
{
	boolean rv = *target;
	*target = TRUE;
	return rv;
}

//process 1
do  
{
	while(TestAndSet(&lock))
	{
		//do nothing
	}
	//critical section
	lock = FALSE;
	//remainder section
	
} 
while (TRUE);

//process 2
do   
{
	while(TestAndSet(&lock))
	{
		//do nothing
	}
	//critical section
	lock = FALSE;
	//remainder section
	
} 
while (TRUE);



```
