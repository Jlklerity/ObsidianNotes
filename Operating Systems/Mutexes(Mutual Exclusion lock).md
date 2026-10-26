
### Also: [[pthread mutex]]

## Boolean variable indicating if lock is available or not
## Doesn't allow multiple threads to access the same data at once. 

## Makes threads take turns when they touch the same data or resource

## Guarantees that a block of code runs without another thread interfering


```c
#include <mutex>

std::mutex m;
int count = 0;

void increment() {
    std::lock_guard<std::mutex> lock(m);   // locks here, unlocks automatically at scope exit
    ++count;
}
```

## Protects a critical section by first acquire() then release() lock

![[Pasted image 20261022162759.png|317]]

## Con: Requires [[busy waiting]]

