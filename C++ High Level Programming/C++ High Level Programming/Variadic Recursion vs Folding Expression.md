	
	
	//Recursive
	template<typename T, typename... Args>
	T sum(T first, Args... rest) {
	    return first + sum(rest...); // Triggers recursive compilation
	}
	//Folding
	template<typename... Args>
	auto sum(Args... args) {
	    return (... + args); // Unary Left Fold: expands to (arg1 + arg2 + ... + argN)
	}