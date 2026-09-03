

> [!note]
> Non-owning/Observing pointers that do not increase the reference count of a shared pointers when is pointing at one.
>
> Allows to safely destroy the shared pointer and the weak pointer will expire and no longer observe the shared pointer's underlying data  (lifetime of the underlying data would still be around if it was a shared pointer pointing to it instead) 
	
	#include <iostream>
	#include <memory> 
	
	class UDT {
	public:
	    UDT() { std::cout << "UDT Created" << std::endl; }
	    ~UDT() { std::cout << "UDT Destroyed" << std::endl; }
	};
	
	int main() {
	    std::weak_ptr<UDT> ptr2;
	    {
	        std::shared_ptr<UDT> ptr1 = std::make_shared<UDT>();
	        {
	            // Share the resource with a weak_ptr
	            ptr2 = ptr1;
	            // Reference count is NOT updated by weak_ptr
	            std::cout << "(inside scope) use count = " << ptr2.use_count() << std::endl;
	            // .lock() creates a temporary shared_ptr, safely bumping the count to 2
	            if (std::shared_ptr<UDT> temp = ptr2.lock()) {
	                std::cout << "Data is alive!\n";
	            } 
	            // The 'if' block ends here. 'temp' is destroyed, dropping the count back to 1.
	            // (Note: ptr2 is NOT freed here. It lives until the end of main).
	            // We check our updated reference count
	            std::cout << "use count = " << ptr1.use_count() << std::endl;
	        }
	        
	    } // ptr1 goes out of scope here. Count hits 0. "UDT Destroyed" is printed.
	    std::cout << "Is weak_ptr expired? " << ptr2.expired() << std::endl;
	    return 0;
	}

	Output :
	UDT Created
	(inside scope) use count = 1
	Data is alive!
	use count = 1
	UDT Destroyed
	Is weak_ptr expired? 1
	
> [!question] .lock()
> temporarily converts a weak_ptr into a shared_ptr so you can safely use the data.
