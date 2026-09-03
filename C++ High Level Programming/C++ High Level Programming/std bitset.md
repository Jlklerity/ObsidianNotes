

	
	int main() {
	    
	    // 18 = (10010)
	    std::bitset<5> bs(18);
	    
	    // Check 3rd bit
	    std::cout << bs[2] << endl;
	    
	    // Check 5th bit
	    std::cout << bs.test(4);
	    return 0;
	}
	//output
		0
		1

> [!note] Using .test() vs accessing data with subscripts
> bs[2] does not perform bounds checking. If you ask for an index larger than your bitset (like bs[10]), it results in undefined behavior. It is slightly faster.
> 
> bs.test(4) does perform bounds checking. If you ask for an out-of-bounds index (like bs.test(10)), it <font color="#ffff00">safely throws a std::out_of_range exception</font>.
> 
