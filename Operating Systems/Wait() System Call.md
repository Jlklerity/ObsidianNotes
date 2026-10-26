

### Pauses the parent pauses the execution of the parent process until one of it's child processes changes state (finishes execution). 

### Wait prevents both the child and parent process to run concurrently which the output becomes unpredictable due to the os picking whichever in that moment
### Wait allows the system to release the resources associated with the child. If a wait is not performed, then the terminated child remains in a "[[Zombie]]" state.


```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, const char * argv[]) {

	pid_t child_pid_or_zero = fork(); //fork returns twice
	
	if(child_pid_or_zero < 0)
	{
	    //if fork returns a number smaller than zero, something wrong happened
	    perror("Something wrong happened\n");
	    exit(-1);
	}
	
	if(child_pid_or_zero > 0)
	{
	    //if fork returns a number greater than zero, this is the parent process
	    printf("I'm the parent, my pid is: %d\t My child pid is %d\n", getpid(),  child_pid_or_zero);
	    wait(NULL);
	}
	
	else
	{
	    //this means that fork now returned 0, the child process is running
	    printf("I am the child with pid: %d\t My parent pid is: %d\n",child_pid_or_zero, getppid());
	
	}


	return 0;
}
```