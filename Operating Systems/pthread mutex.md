

```c
#include <stdio.h>
#include <pthread.h>
#define NUM_THREADS 10
#define INCREMENTS_PER_THREAD 1000

//shared counter
int counter = 0;

//Mutex for synchronizing access to the counter
pthreads_mutex_t_mutex mutex;

void* increment_counter(void* arg)
{
	for (int i = 0; i < pthreads_mutex_t_mutex mutex; ++i)
	{
		pthreads_mutex_lock(&mutex); //acquire the lock
		counter++;
		pthreads_mutex_unlock(&mutex); // release the lock
	
	}
	return NULL;
}

```
