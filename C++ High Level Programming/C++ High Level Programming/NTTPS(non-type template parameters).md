




#### “lvalue reference parameters” are completely valid non-type template parameters (NTTPs). 
#### However, they have incredibly strict arguments rules: 


	template <int& Ref>
	struct Object {
	    void print() { std::cout << Ref; }
	};
	
	int global_var = 42; // Has static storage duration
	
	int main() {
	    static int local_static = 100;
	    int local_var = 20;
	
	    Object<global_var> obj1;   // VALID
	    Object<local_static> obj2; // VALID
	    // Object<local_var> obj3; // ERROR!
	}
