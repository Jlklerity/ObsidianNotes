
	#include <cstdarg>
	#include <iostream>
	
	int sum(int count, ...){
	    if(count <= 0){
	        return 0;
	    }
	    va_list argp;
	    va_start(argp, count);
	
	    int total{};
	    while(count--){
	        int value = va_arg(argp, int);
	        total += value;
	    }
	
	    va_end(argp);
	    return total;
	}
	
	int main(){
	    std::cout<<"total: "<< sum(1,3)<< '\n';
	}