
> [!note]
> For NRVO to occur, the C++ standard requires the return expression to be the unparenthesized name of a local variable with the same type as the function's return type.


`int foo(int i){ //RVO`
	 `return i;`
`}`

`int foo(){  //RVO`
	`return int{1}`
`}`

`int foo(int i){ //NRVO`
	`int j = i;`
	 `return j;`
`}`

`int foo(int i){     //NOT COPY ELISION since the compiler needs to decide during the if statement`
	 `if(i % 2){`
		 `return i;`
	 `}`
	 `return 0;`
`}`

`int foo(int i){`
		`return std::move(i); //NVRO DISABLED due to std::move()`
`}`
