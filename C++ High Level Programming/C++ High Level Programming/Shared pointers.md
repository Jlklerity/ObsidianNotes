
> [!note]
> Unlike **unique_ptr**s that demands **exclusive ownership** of its data. `Shared_ptrs` can point to the **same underlying data**.

> [!important] Reference Count (use_count)
> The reference count is a check for the shared pointer to know how many shared pointers are pointing to the same underlying data 


> 
	
	class UDT{
	public:
	    UDT() { std::cout << "UDT Created" << std::endl; }
	    ~UDT() { std::cout << "UDT Destroyed" << std::endl; }
	};
	
	int main(){
	    std::shared_ptr<UDT> ptr1 = std::make_shared<UDT>();
	    std::shared_ptr<UDT> ptr2 = ptr1;
	    std::shared_ptr<UDT> ptr3 = ptr1;
	    std::shared_ptr<UDT> ptr4 = ptr3;
	    
	    std::cout<< "use count ptr1: "<<ptr1.use_count()<<'\n'; 
	    std::cout<< "use count ptr4: "<<ptr4.use_count()<<'\n';
	    return 0;
	    
		 Output: 
		  UDT Created
		  use count ptr1: 4
		  use count ptr4: 4
		  UDT Destroyed

	}


> [!note] Why only one Constructor and Destructor called?
> since all the shared pointers are pointing to the same underlying data, only one construction of clas UDT has to be made to allocate memory for that once underlying data.
> 
> The memory will then be freed when the reference count goes to 0
