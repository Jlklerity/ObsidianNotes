# Basic Steps and Input Size

> [!question] Why not just measure seconds?
> [[Wall-clock time]] depends on the CPU, the language and compiler, and
> implementation details. We want a machine-independent measure instead.

> [!info] Definition — running time
> The step count $T(n)$ of an algorithm is the **number of basic steps**
> it performs on an input of size $n$. Which is a more consistent measurement of speed of an algorithm through different hardware, compared to using Wall-Clock time.

## What counts as a basic step

> [!info] Definition — basic step
> One instruction a processor executes directly on values of a **fixed
> number of bits** (e.g. a 32-bit integer).
> 
> For example:
> ar[h-1] is considered one step to find the value in ar 
> ar[h-1] followed by another line ar[h-2] now takes two steps to find the first and second value in ar.

Three families (typical, not exhaustive):

| Family               | Examples                                                  |
| -------------------- | --------------------------------------------------------- |
| Arithmetic           | `+ - * /`, remainder, floor, ceiling, shifts, bitwise ops |
| Comparison & control | `< <= == !=`, branching, calling, returning               |
| Data movement        | reading/writing `A[i]`, assigning to a variable           |

Because a basic step works on a fixed number of bits, it takes **constant
time**, independent of how much data the algorithm processes.

> [!note] Word-RAM model
> Week 01's assumption (reading `A[i]` costs the same whatever the index)
> plus this week's assumption (each basic step is constant time) together
> define the **word-RAM model**. A *word* is the fixed-width chunk of data
> the machine handles in one step.

## How input size is measured

Input size describes how "big" the problem instance is. It depends on the
problem — and it is **not always a single number**.

| Problem | Input size |
|---|---|
| Sorting | $n$ = number of keys in the array |
| Matrix multiplication | $n$ = rows/columns of an $n \times n$ matrix — the input holds $n^2$ numbers, not $n$ |
| Graph algorithms | **two** parameters: $\|V\|$ vertices and $\|E\|$ edges |

> [!warning] A bound like $O(\|V\| + \|E\|)$ cannot be written with a single
> $n$ at all. Don't assume input size is one number.

---
Next: [[Running Times (n) of non-recursive algorithms]]
