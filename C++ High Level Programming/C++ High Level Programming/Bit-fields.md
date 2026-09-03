
	
	//Optimizing each member of struct to have a specified amount of bits
	struct PlayerAttributes {
		using UI = uint32_t;
		UI level : 2; // 0 - 3
		UI power : 6; // 0 - 63
		UI range : 10; // 0 - 1023
		UI armor : 4; // 0 - 15
		UI health : 9; // 0 - 511
		UI grade : 1; // 0 - 1
	};