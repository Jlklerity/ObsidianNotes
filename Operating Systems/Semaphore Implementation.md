

```c
void wait()  //P
{
	while (TestAndSet(&lock))
	{
		add self process to queue;
		lock = false;
		block(&lock);
	}
	s--;
	lock = false;
}

void signal() //V
{
	while (TestAndSet(&lock))
	{
		s++;
		if (queue is not empty)
			wake up any process waiting in queue
		
		lock = false;
	}

}
```

