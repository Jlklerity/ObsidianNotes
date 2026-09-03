

	#include <iostream> 
	#include <vector> 
	#include <list>  
	#include <algorithm>

	std::list<int> const src{1, 2, 3, 4, 5};  
	int const tgt_val {4};  
	std::vector<int> dst(std::begin(src), std::end(src));  
	void print(std::vector<int>& c, const char* ch){  
		std::cout<<ch;  
		for(int& u : c){  
			std::cout<<u<<' ';  
		}  
			std::cout<<'\n';  
	}  
	int main(){  
		std::vector<int>::iterator it = std::find(dst.begin(), dst.end(), tgt_val);
	    std::for_each(it, dst.end(), [](int& value){
	        value = 0;
	    });
      
	    print(dst, "dst: "); 
	    
	    std::for_each(dst.begin(), dst.end(), [](int& value){
	        value = 2;
	    });
	    print(dst, "dst: ");
    }
	 output:
	 dst: 1 2 3 0 0 
     dst: 2 2 2 2 2 
