

	#include <variant>
	#include <iostream>
	 
	union Data {
	    int i;
	    float s;
	};
	 
	int main(){
	    Data a{'c'};
	    std::cout<<"sizeof(Data) = "<<sizeof(a)<<'\n'; 
	    std::cout<< a.i<<'\n';
	
	    std::variant<int,char> Safer_Data{5};
	    std::cout<<"sizeof(Safer_Data) = "<<sizeof(Safer_Data)<<'\n';
	    std::cout<< std::get<int>(Safer_Data);
	}
		Output:
		  sizeof(Data) = 4
		  99
		  sizeof(Safer_Data) = 8
		  5
> [!important]
> std::variant will throw an exception if the value you assign to it is not the exact same type. Wheareas a Union will allow the data to be implicit


## std::variant under the hood

	struct VariantUnderTheHood {
	    // 1. A union forces the types to share the same memory address
	    union {
	        int num;
	        std::string str;
	    };
	    
	    // 2. The tag to remember what is currently in the union
	    int tag; 
	
	    // Constructor for int
	    VariantUnderTheHood(int n) : num(n), tag(0) {}
	
	    // Constructor for string
	    VariantUnderTheHood(const std::string& s) : str(s), tag(1) {}
	
	    // Destructor (Crucial!)
	    ~VariantUnderTheHood() {
	        if (tag == 1) {
	        // Because it's a union, the compiler doesn't know which destructor 
	            // to call. We have to call the string destructor manually.
	            str.~basic_string(); 
	        }
	    }
	};