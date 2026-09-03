

> [!attention]
> Compilers must align strucuture objects based on largest data member type!

	struct Weapon { 
		char name[81]; 
		int32_t damage; 
		float range; 
	};
	   Objects of type Weapon are given storage at addresses divisible by 4 since          they contain int32_t and float data members

![[Pasted image 20260801181011.png]]

![[Pasted image 20260801182024.png]]
## Suppressing Default Padding

![[Pasted image 20260801181232.png]]