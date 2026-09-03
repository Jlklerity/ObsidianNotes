


	#include <iostream>
	#include <cstddef>
	
	int main() {
	    std::byte b1{0b10100000};
	    std::byte b2{0b00001111};
	
	    // Bitwise OR
	    std::byte b3 = b1 | b2; 
			std::byte b4 = b1 & b3;
			
	    // Explicitly convert to an integer for printing
	    std::cout << std::to_integer<int>(b3) << "\n"; // Output: 175
			std::cout << std::to_integer<int>(b4) << "\n"; // Output: 0
	
	    return 0;
	}


## Why use std::byte?

> [!note]
> std::byte forces bitwise operations and reinforces bit twiddling semantics
> 
> better than using unsigned or signed char

	constexpr std::byte b{1};
	constexpr auto b1 = b << 7;
	
	static_assert(std::to_integer<int>(b) == 0x01);
	
	// Increment pointer
	uint8_t read(char* c, int offset) {
	    return *(c + offset); //COMPILES
	}
	
	uint8_t readMistake(char* c, int offset){
	    return *c + offset; //no compile-error since its a char
	}
	std::byte read(std::byte* b, int offset){
	    return *(b + offset); //COMPILES
	}
	
	std::byte readMistake(std::byte* b, int offset){
	    return *b + offset; //COMPILE ERROR SINCE STD::BYTE TYPES CANT USE 
											    //ARITHMETIC OPERATORS AND ONLY  BITWISE OPERATORS
	}