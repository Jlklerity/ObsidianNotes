

> [!note] Why is it used?
> The most significant practical benefit of noexcept is enabling move semantics during container reallocations.

|**Situation**|**Behavior**|
|---|---|
|**Move Constructors / Assignments**|Mark `noexcept` so STL containers use fast moves.|
|**Destructors**|`noexcept` by default in C++11 and later. Never throw from a destructor.|
|**Swap Functions**|Should almost always be `noexcept`.|
|**Functions that _might_ fail**|Do **not** mark `noexcept` unless you intend to terminate on failure.|
