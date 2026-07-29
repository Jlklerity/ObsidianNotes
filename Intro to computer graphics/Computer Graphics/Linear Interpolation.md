

![[Pasted image 20260722125407.png|353]]

$$
  

s = \left(\frac{t_2 - t}{t_2 - t_1}\right)s_1 + \left(\frac{t - t_1}{t_2 - t_1}\right)s_2
$$
$$
\left(\frac{t_2 - t}{t_2 - t_1}\right) leftweight, \left(\frac{t - t_1}{t_2 - t_1}\right) rightweight
$$

> [!info]
> Adding the two weights MUST add up to 1, ensuring that s stays proportionally bounded between s1 and s2.

$$
  

\frac{t_2 - t}{t_2 - t_1} + \frac{t - t_1}{t_2 - t_1} = \frac{t_2 - t + t - t_1}{t_2 - t_1} = \frac{t_2 - t_1}{t_2 - t_1} = 1
$$

`template <typename T>`
	`T mix(T s1, T s2, double t) {`
	`return s1*(1.0 - t) + s2*t;`
`}`