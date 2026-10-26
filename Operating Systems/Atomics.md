
## Protects one variable and one operation at a time all doesnt allow any other process to interrupt until the process running the [[critical section]] has finished execution



```c
#include <atomic>

std::atomic<int> count{0};

void increment() {
    ++count;                 // atomic read-modify-write, no mutex needed
    // or: count.fetch_add(1);
}

int x = count.load();        // atomic read
count.store(5);              // atomic write
```
