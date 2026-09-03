
	#include <iostream>
	#include <type_traits>
	
	
	template<typename T>
	struct is_integral { static constexpr bool value = true; };
	
	template<>
	struct is_integral<double> { static constexpr bool value = false; };
	
	template<>
	struct is_integral<unsigned long long> { static constexpr bool value = true; };
	
	template<typename T>
	constexpr bool is_integral_v = is_integral<T>::value; 
	
	int main(){
	    std::cout<<(is_integral<int>::value == false);
	    std::cout<<(is_integral_v<int> == true);
	    std::cout<<(is_integral_v<double> == false);
	    std::cout<<(is_integral_v<unsigned long long> == true);
	    
	}
		Output:
		  0111