

## [[Static Hash Table Code]] 

## [[Universal Hash Table Code]] (best practice)


### stores keys in an array. A hash function h converts each key k into an array index h(k), and the key is stored in slot T [h(k)].

|key|h(k) = k mod 11|stored in|
|---|---|---|
|56|1|`T[1]`|
|29|7|`T[7]`|
|90|2|`T[2]`|

### once a key is set, it can be called it directly with an operation time of Θ(1).


### Methods of generating Hash Functions
#### - Division Method (static)

![[Pasted image 20261004155150.png]]

#### - Universal Hashing

![[Pasted image 20261004155224.png]]

##### - Mitigates worse case scenarios where many keys hash onto the same index

> [!note] Are they different?
> ###### Universal hashing still ends with a mod m step, but the function is chosen at random, which is why a bad input set can't be planned in advance.


### Other ways of resolving hash collisions

#### - Chaining
- Each slot holds a pointer to a linked list of all keys that hash to that slot.
- Load factor α = n / m (keys / slots). It is the average length of a list, and it can exceed 1.
- Search takes Θ(1 + α) on average. Insert takes Θ(1). Delete takes Θ(1) with a doubly linked list.

![[Pasted image 20261004155756.png]]

#### - Open Addressing
 - All keys are stored in the table itself, at most one key per slot, so α ≤ 1.
- On a collision, follow the key's probe sequence h(k, 0), h(k, 1), … until an empty slot is found. The sequence must be a permutation of all slots.
- Linear probing: simple, but causes clustering. Double hashing: less clustering.
- Delete by marking the slot `deleted`, never `nil`.
- Expected probes: at most 1/(1 − α) for an unsuccessful search or insert. These bounds blow up as α → 1.