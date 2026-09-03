

## Also known as an interrupt handler, is a special software block of code that automatically executes when a hardware or software signal demands immediate processor attention


### 1. A hardware event (like a keystroke or network packet) or a software exception sends an interrupt signal to the CPU.

### 2. Pause: The CPU pauses its current task and saves its active state or register data.

### 3. Lookup: The CPU uses an interrupt number to find the matching code address inside the system's [[Interrupt Vector Table]]/Interrupt Descriptor Table depending on the CPU's mode.

### 4. Execution: The CPU runs the ISR to clear or manage the urgent device request.

### 5. Resume: The CPU restores the old program state and goes back to the original task.  
 
	