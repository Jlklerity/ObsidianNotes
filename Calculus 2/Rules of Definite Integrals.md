

## Six rules ($c$ is any constant)

### 1. Zero-width interval
$$\int_a^a f(x)\, dx = 0$$

### 2. Swapping limits flips the sign
$$\int_a^b f(x)\, dx = -\int_b^a f(x)\, dx$$

### 3. Integral of a constant
$$\int_a^b c\, dx = c(b-a)$$

### 4. Constant multiple
$$\int_a^b c f(x)\, dx = c \int_a^b f(x)\, dx$$

### 5. Sum and difference
$$\int_a^b [f(x) \pm g(x)]\, dx = \int_a^b f(x)\, dx \pm \int_a^b g(x)\, dx$$

### 6. Splitting the interval (additivity)
$$\int_a^b f(x)\, dx = \int_a^c f(x)\, dx + \int_c^b f(x)\, dx$$

> [!hint] Rule 6 holds for **any** $c$ — it does not have to lie between $a$ and $b$.

> [!question] Sanity-check rules 1 and 3 geometrically
> A definite integral is a net area. What is the area of a region of zero width? Of a rectangle of height $c$ and width $b-a$?

> [!question] Where does rule 2 come from?
> Apply FTC2 to both sides: $F(b) - F(a)$ versus $F(a) - F(b)$.
