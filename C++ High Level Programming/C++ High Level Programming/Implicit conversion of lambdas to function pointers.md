
> [!warning]
> ONLY LAMBDAS WITH <font color="#ff0000">EMPTY CAPTURE LISTS</font> CAN BE CONVERTED TO FUNCTION POINTERS


`int(*func_ptr)(int, int) = [](int a, int b) { return a + b; };`

`struct CompilerGeneratedLambda {`
    `// No member variables! No state to keep track of.`
    `void operator()() const { /* body */ }`

    // Because there is no state, the compiler can safely generate this:
    operator void(*)()() const { return []() { /* body */ }; }
`};`


`struct CompilerGeneratedLambda {`
    `Prime& p; // ⚠️ Stored reference! This object now takes up memory.`

    `CompilerGeneratedLambda(Prime& p_arg) : p(p_arg) {}`

    `void operator()() const { p.add(40); }`

    `// ❌ IMPOSSIBLE: A raw function pointer cannot hold or look up the 'p' reference!`
    `// Therefore, no conversion operator is generated.`
`};`
