

## Step 1: divide $[a, b]$ into $n$ subintervals of equal width

$$\Delta x = \frac{b-a}{n}$$

Label the division points $a = x_0, x_1, x_2, \dots, x_{n-1}, x_n = b$ where
$$x_i = x_0 + i\Delta x$$

The $n$ subintervals are
$$[x_0, x_1],\ [x_1, x_2],\ \dots,\ [x_{n-1}, x_n]$$

### Sample points
- Left endpoints: $x_i^* = x_{i-1}$
- Right endpoints: $x_i^* = x_i$

> [!hint] There are $n+1$ division points but only $n$ rectangles.

> [!question] Test yourself
> On $[4, 14]$ with $n = 40$ rectangles: what is $\Delta x$? Which of $14$, $11.5$, $7.75$, $7$, $5.55$ is **not** a right endpoint?
> Method: a value $v$ is a right endpoint only if $\frac{v - a}{\Delta x}$ is a whole number between $1$ and $n$.
