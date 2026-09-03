

![[Pasted image 20260802131706.png|476]]
COMPILES: because copy constructor/assignment operator exists so it will default back to it


--------------------------------------------------------------------------
![[Pasted image 20260802131724.png|485]]
COMPILE ERROR: because the copy assignment is deleted and move assignment is not declared


--------------------------------------------------------------------------
![[Pasted image 20260802131822.png]]
COMPILE ERROR: because the move assignment operator is explicitly deleted


--------------------------------------------------------------------------
![[Pasted image 20260802131913.png|696]]
COMPILE ERROR: class contains data that cannot be moved or copied causing the class to have implicit copy & move constructors/ assignment operators deleted.