

## Let $c$ and $k$ be constants.

### Structural rules
$$\int c f(x)\, dx = c \int f(x)\, dx$$
$$\int [f(x) \pm g(x)]\, dx = \int f(x)\, dx \pm \int g(x)\, dx$$

### Powers, exponential, logarithm
$$\int k\, dx = kx + C$$
$$\int x^n\, dx = \frac{x^{n+1}}{n+1} + C \qquad (n \neq -1)$$
$$\int e^x\, dx = e^x + C$$
$$\int \frac{1}{x}\, dx = \ln|x| + C$$

### Trigonometric
$$\int \sin x\, dx = -\cos x + C$$
$$\int \cos x\, dx = \sin x + C$$
$$\int \sec^2 x\, dx = \tan x + C$$
$$\int \sec x \tan x\, dx = \sec x + C$$

### Inverse trigonometric
$$\int \frac{1}{\sqrt{1-x^2}}\, dx = \sin^{-1} x + C$$
$$\int \frac{1}{1+x^2}\, dx = \tan^{-1} x + C$$

> [!warning] These are only valid on an interval where the **integrand is continuous**.

> [!question] Why is $n = -1$ excluded from the power rule?
> Substitute $n = -1$ into $\frac{x^{n+1}}{n+1}$ and see what breaks. That hole is exactly why $\ln|x|$ gets its own line.

> [!question] Why $\ln|x|$ and not $\ln x$?
> What is the domain of $\frac{1}{x}$, and what is the domain of $\ln x$?
