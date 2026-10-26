```c
#include <iostream>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    int result = 0;
    int fd[2]; // fd[0] is for reading, fd[1] is for writing

    // Create a pipe before forking
    if (pipe(fd) == -1) {
        std::cerr << "Pipe failed\n";
        return 1;
    }

    int pid = fork();

    if (pid == 0) {
        // --- Child Process ---
        close(fd[0]); // Close the unused read end

        std::cout << "Child: I will add 1 + 1...\n";
        result = 1 + 1; // Perform calculation

        // Send the result to the parent through the pipe
        write(fd[1], &result, sizeof(result));
        close(fd[1]); // Done writing
        
        return 0;
    } 
    else if (pid < 0) {
        std::cerr << "Fork failed\n";
        return 1;
    } 
    else {
        // --- Parent Process ---
        close(fd[1]); // Close the unused write end
		
        int status{};
        wait(&status); // Wait for child to finish
	
        // Read the result sent by the child from the pipe
        read(fd[0], &result, sizeof(result));
        close(fd[0]); // Done reading

        std::cout << "Parent: The child passed me the result!\n";
        std::cout << "Parent: btw the result is " << result << '\n'; 
        // This will now print: Parent: btw the result is 2
    }
    return 0;
}
