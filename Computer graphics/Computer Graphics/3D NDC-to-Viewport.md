
![[Pasted image 20260727122619.png]]
![[Pasted image 20260727122653.png]]
![[Pasted image 20260727125231.png]]

| **Axis** | **NDC Range** | **Viewport Target Range**       | **Scale Factor**   | **Shift / Offset**             | **Final Formula**                      |
| -------- | ------------- | ------------------------------- | ------------------ | ------------------------------ | -------------------------------------- |
| **X**    | $[-1, 1]$     | $[x_{bl}^d, x_{bl}^d + W_{vp}]$ | $\frac{W_{vp}}{2}$ | $+\frac{W_{vp}}{2} + x_{bl}^d$ | $\frac{W_{vp}}{2}(1 + x_n) + x_{bl}^d$ |
| **Y**    | $[-1, 1]$     | $[y_{bl}^d, y_{bl}^d + H_{vp}]$ | $\frac{H_{vp}}{2}$ | $+\frac{H_{vp}}{2} + y_{bl}^d$ | $\frac{H_{vp}}{2}(1 + y_n) + y_{bl}^d$ |
| Z        | $[-1, 1]$     | $[0, 1]$                        | $\frac{1}{2}$      | $+\frac{1}{2}$                 | $\frac{1}{2}(1 + z_n)$                 |

> [!question] Why does Z axis only translate by dividing by 2?
> In Viewport to the screen, the dimensions are 2D, therefore we have to do an additional translation of moving X and Y to the origin (0,0) of the viewport.
> 
> Z is not considered in 2D so it simply just divides by 2
