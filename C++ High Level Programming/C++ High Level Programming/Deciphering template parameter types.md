
> [!hint]
> If you rely on compiler deduction (like calling a function template), the compiler strips references by design.

	template <typename T>
	void f(T& t) {
	  std::cout << t;
	}
	
	int main(){
	    int i{42}, &r1{i}, *p1{&i}, *&r2{p1};
	    int const i2{i}, &r3{i2}, *p2{&i2}, *&r4{p2};
	    f(r2);
	}
       
		argument type?     template parameter T's type?      parameter t?   
	f(i) :    int,                 int,                         int&
	f(r1):    int&,                int,                         int& 
	f(p1):    int*,                int*,                        int*&
	f(*p1):   int,                 int,                         int&
	f(r2):    int*&,               int*,                        int*&
	f(*r2):   int,                 int,                         int&
	f(i2):    int const,           int const,                   int const&
	f(r3):    int const&,          int const,                   int const&
	f(p2):    int const*,          int const*,                  int const*&
	f(*p2):   int const,           int const,                   int const&
	f(r4):    int const*&,         int const*,                  int const*&
	f(*r4):   int const&,          int const,                   int const&

