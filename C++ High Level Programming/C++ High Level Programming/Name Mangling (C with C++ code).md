
![[Pasted image 20260730130318.png|232]]![[Pasted image 20260730130322.png|460]]

![[Pasted image 20260730130107.png|418]]

> [!note]
> Since C++ has Function Overloading, the compiler gives a mangled name for each of the overloaded functions. Since C Compiler doesn’t provide mangled names, we need to use **Extern “C”** on the C++ functions to prevent mangled names from being made by the compiler, forcing it to use C-style linkage.
> 

> [!hint] USE POLYGLOT HEADERS (BEST PRACTICE)
> **__cplusplus is only recognized in C++, so it won’t affect C code when checking.**
> 
> ![[Pasted image 20260730130227.png]]



