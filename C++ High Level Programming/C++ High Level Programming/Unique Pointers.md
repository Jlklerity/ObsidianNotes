
> [!note]
> Unique pointers are used when we only want a set of data to be owned exclusively by one pointer


	#include <iostream>
	#include <memory>
	template <typename T>
	class Proxy {
	    using pointer = std::unique_ptr<T>;
	    using reference = std::unique_ptr<T>&;
	public:
	    Proxy(T x) : ptr{std::make_unique<T>(x)} {};
	    
	    T& get() const {
	        return *ptr;
	    }
	    
	private:
	    pointer ptr;
	    
	};
	
	template <typename T>
	std::ostream& operator<<(std::ostream& os, Proxy<T>& rhs) {
	    os << (rhs.get());
	    return os;
	}
	int main() {
	    Proxy<int> a {5};
	    std::cout<< a;
	}