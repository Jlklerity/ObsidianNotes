

## Prevents Infinite Loops & Resource Hogging
##### stops a rogue or malfunctioning user program from running indefinitely or monopolizing CPU time.

## Regaining Control / Preemption
##### It is set up before scheduling a process so that the OS can automatically regain control once the program's allotted time slice expires.

## Terminate Overdue Programs
##### It allows the OS to terminate or deschedule programs that exceed their allowed execution time.


**How It Works:**

1. The OS sets a hardware counter to a specific value using a privileged instruction.
    
2. The counter is continuously decremented by the physical clock ticks.
    
3. When the counter reaches zero, the hardware generates an interrupt, transferring control back to the OS kernel.