
![[Pasted image 20261026220027.png]]
## Also known as [[Bounded-Buffer]] problem


## The producer process and the consumer processs are race conditioning against one another to increment(the producer) and decrement(the consumer) the buffer. <font color="#ffff00">This is if there isnt a Mutexes(Mutual Exclusion lock) to make the other process wait.</font>

## The consumer is notified that the mutex is unlocked and accessible for execution in the critical section using a [[Condition Variable]].



![[Pasted image 20261026221813.png]]

![[Pasted image 20261026221830.png|700]]

![[Pasted image 20261026221857.png|700]]

![[Pasted image 20261026221930.png]]