



	#include <type_traits>
	#include <cmath>
	#include <iostream>
	
	struct Monster{
	    int strength;
	    int health;
	};
	
	struct False_Type {
	    static constexpr bool value = false;
	};
	
	struct True_Type {
	    static constexpr bool value = true;
	};
	
	template<typename T>
	struct is_monster : False_Type{};
	
	template<>
	struct is_monster<Monster> : True_Type{};
	
	int main(){
	    float f = 0.0f;
	    std::cout<<"float: "<<(std::is_floating_point<float>::value)<<'\n';
	    std::cout<<"float: "<< (std::is_floating_point_v<float>)<<'\n';
	    std::cout<<"f: "<< (std::is_floating_point_v<decltype(f)>)<<'\n';
	    
	    int i = 0.0f;
	    
	    std::cout<<"int: "<< (std::is_floating_point<int>::value)<<'\n';
	    std::cout<<"int: "<< (std::is_floating_point_v<int>)<<'\n';
	    std::cout<<"i: "<< (std::is_floating_point_v<decltype(i)>)<<'\n';
	    
	    Monster m;
	    
	    std::cout<<"i: "<< (is_monster<int>::value)<<'\n';
	    std::cout<<"m: "<< (is_monster<decltype(m)>::value)<<'\n';
	}