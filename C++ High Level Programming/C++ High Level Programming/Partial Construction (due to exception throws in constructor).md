

|**Constructor Type**|**Where Exception Throws**|**Is it "Fully Constructed"?**|**Does Destructor Run?**|
|---|---|---|---|
|**Standard**|Inside its own body or initializer list|**No**|**No** (Only successfully built member variables are cleaned up)|
|**Delegating**|Inside the _delegating_ body (after the target constructor finished)|**Yes**|**Yes** (The entire destructor runs to clean up the object)|

`#include <iostream>`
`#include <string>`
`#include <stdexcept>`
`#include <optional>`

`class Component {`
`public:`
    `Component(std::string name) : name_(name) { std::cout << name_ << " built\n"; }`
    `Component(Component const& other) : name_(other.name_ + " (copy)") {` 
        `throw std::runtime_error("Component not allowed to be copied");`
    `}` 
    `~Component() { std::cout << name_ << " destroyed\n"; }`
`private:`
    `std::string name_;`
`};`

`class MyClass {`
    `Component c1;`
    `std::optional<Component> c2; // Wrapped in std::optional`
    `Component c3;`
`public:`
    `MyClass() : c1("Member 1"), c3("Member 3") {`
        `// c1 and c3 are already fully constructed at this point`
        `try {`
            `c2.emplace(c1); // Attempt to copy-construct c2`
        `} catch (std::runtime_error const& e) {`
            `std::cout << "c2 construction failed gracefully: " << e.what() << '\n';`
        `}`
        `std::cout << "Constructor body reached safely!\n";`
    `}`
    `~MyClass() { std::cout << "MyClass destructor\n"; }`
`};`

`int main() {`
    `MyClass a;`
`}`

`Output:` 
`Member 1 built`
`Member 3 built`
`c2 construction failed gracefully: Component not allowed to be copied`
`Constructor body reached safely!`
`MyClass destructor`
`Member 3 destroyed`
`Member 1 destroyed`

### Execution Flow:

1. **`c1` constructs** $\rightarrow$ `"Member 1 built"`
    
2. **`c2` default-initializes** as an empty `std::optional` (no exception thrown).
    
3. **`c3` constructs** $\rightarrow$ `"Member 3 built"`
    
4. **Constructor Body:** `c2.emplace(c1)` attempts the copy constructor and throws. The `try-catch` inside the constructor body catches and swallows the exception.
    
5. **Destruction:** When `a` goes out of scope, both `c3` and `c1` are properly destroyed in reverse order of declaration.