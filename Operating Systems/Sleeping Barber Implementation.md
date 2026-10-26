![[Pasted image 20261026215648.png]]

```c
Semaphore barbers = 0; 
Semaphore mutex = 1; 
Semaphore customers = 0; 
int nFreeWRSeats = N;

void Barber()
{
	while(1)
	{
		wait(customers);
		wait(mutex);
		nFreeWRSeats++;
		signal(barbers);
		signal(mutex);
		haircut();
	}

}

void Customers()
{
	wait(mutex);
	if (nFreeWRSeats > 0)
	{
		nFreeWRSeats--;
		signal(customers);
		signal(mutex);
		wait(barbers);
		get_haircut();
	
	}
	else
	{
		signal(mutex);
		leaveWR();
	}

}


```

