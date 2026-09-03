

- **Top-level `const` (Stripped):** <font color="#ff0000">The `const` applies to the variable itself</font>.
    - `const int` decays to `int`.
    - `int* const` (a constant pointer to a modifiable integer) decays to `int*`. The pointer itself is no longer constant.
    
- **Low-level `const` (Preserved):** <font color="#ff0000">The `const` applies to the data being pointed to or referenced</font>.
    - `const int*` (a modifiable pointer to a constant integer) decays to **`const int*`**. It does _not_ strip the `const` because the `const` belongs to the underlying integer, not the pointer