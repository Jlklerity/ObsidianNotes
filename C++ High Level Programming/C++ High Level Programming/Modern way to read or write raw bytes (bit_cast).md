
![[Pasted image 20260730130714.png]]

> [!question] How it works
> bit_cast is safer since both original and newly bitwise-copied object must be **the same byte size.**
> 
> bit_cast **creates a new object buffer** of the wanted data_type and stores the data into the buffer, unlike reinterpret_cast that uses the same data and only changes the compiler’s interpretation of that data (pointer type)
> 
> use .data() to get the pointer of the data before .read() and .write() for reading or writing data from memory of raw bytes
> 
> .data() gives the stream the raw memory address of that array's first element.
> 
]

![[Pasted image 20260730130719.png]]