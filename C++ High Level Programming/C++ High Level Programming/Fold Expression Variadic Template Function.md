
	
	template<typename T, typename ...Args>
	void print(std::ostream& os, T first, Args... args){
	    os << first;
	    ((os << args << ' '), ...);
	    os << '\n';
	}
	
	
	int main(){
	   //print(std::cout);                 // compile-time error
	    print(std::cout, '1');              // prints 1, followed by newline
	    print(std::cout, 1, 2.0);           // prints 1, 2, followed by newline
	    print(std::cout, 1, 2.0, '3', "4"); // prints 1, 2, 3, 4, followed by newline
	    print(std::cout, 7.5, "hello", "sunshine", std::bitset<16>(377), 42); // prints 7.5,hello,sunshine,0000000101111001,42, followed by newline
	}