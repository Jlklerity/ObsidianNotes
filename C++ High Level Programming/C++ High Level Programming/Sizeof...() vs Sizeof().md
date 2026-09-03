


| **Feature [[1](https://www.youtube.com/watch?v=2wNc15926X4), [2](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/sizeof), [3](https://www.linkedin.com/pulse/why-sizeof-called-operator-function-c-arshad-hussain-z1awc), [4](https://www.scaler.com/topics/c/size-of-in-c/), [5](https://www.reddit.com/r/C_Programming/comments/1k8l0ro/why_sizeofarray_works_in_main_but_not_in_function/)]** | **`sizeof`**                                   | **`sizeof...`**                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- | ------------------------------- |
| **Primary Purpose**                                                                                                                                                                                                                                                                                                                                                                                                           | Returns **size in bytes**.                     | Returns **count of arguments**. |
| **Operand Type**                                                                                                                                                                                                                                                                                                                                                                                                              | A specific data type, variable, or expression. | A template parameter pack.      |
| **Language Support**                                                                                                                                                                                                                                                                                                                                                                                                          | Standard C and C++.                            | C++11 and newer only.           |
| **Evaluation Time**                                                                                                                                                                                                                                                                                                                                                                                                           | Almost always compile-time.                    | Strictly compile-time.          |
| **Return Type**                                                                                                                                                                                                                                                                                                                                                                                                               | `std::size_t`.                                 | `std::size_t`.                  |

	int x = 42;
	int arr[10];
	
	std::size_t size_of_int = sizeof(int);  // Returns 4 (usually)
	std::size_t size_of_x   = sizeof x;     // Returns 4 (parentheses optional)
	std::size_t size_of_arr = sizeof(arr); // Returns 40 (10 elements * 4 bytes)
	
	// A variadic template function
	template <typename... Args>
	void countArguments(Args... args) {
	    // Counts how many types are in the parameter pack
	    std::size_t type_count = sizeof...(Args);
	    
	    // Counts how many function arguments are in the value pack
	    std::size_t value_count = sizeof...(args);
	
	    std::cout << "Arguments passed: " << value_count << "\n";
	}
	
	int main() {
	    countArguments(1, 2.5, 'a', "hello"); // Prints: Arguments passed: 4
	}
