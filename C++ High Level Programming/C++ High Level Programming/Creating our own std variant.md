

	#include <variant>
	#include <iostream>
	 
	struct IntOrString {
	    int num;
	    std::string str;
	    int tag;
	    
	    IntOrString(int n) : num{n}, tag{0} {}
	    IntOrString(const char* s) : str{s}, tag{1} {}
	    IntOrString(const std::string& s) : str{s}, tag{1} {}
	    
	    int index() const {
	        return tag;
	    }
	};
	
	//using IntOrString = std::variant<int, std::string>;

		// We either use struct IntOrString OR use std::variant version
	IntOrString make_variant(bool use_int, int int_val, const std::string& str_val){
	    if(use_int){
	        return IntOrString(int_val);
	    }
	    else{
	        return IntOrString(str_val);
	    }
	}
	
	int main(){
	    make_variant(true, 42, "ignored");  // holds int 42
	    make_variant(false, 0, "hello");    // holds string "hello"
	}