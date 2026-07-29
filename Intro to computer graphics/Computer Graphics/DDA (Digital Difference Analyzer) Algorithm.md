

> [!important]
> The slope cannot exceed 1 along a given axis, if so, the other axis will need to be considered to get the slope within 0 to 1 (applies to ascending slopes, -1 to 0 for descending)

![[Pasted image 20260722144440.png]]
(0<m<1) Only one pixel is considered as intended

![[Pasted image 20260722121910.png|240]]
(m > 1) Now two pixels are considered, but the pixel above is ignored due to the algorithm)

![[Pasted image 20260722121933.png|518]]

> [!tip] Con
> Limited Precision and Accumulates Errors

`//ONLY FOR 0 <= m <= 1`
`int dx = x2 - x1, dy = y2 - y1;`
`double m = (double)(dy)/(double)(dx); //slope`
~~`double h = y1 - m*x1; //y-intercept`~~
`set_pixel(x1, y1, color); //starting pixel at the origin`
`int x = x1;`
`double y = (double)y1;`
`while(--dx) {`
	`++x;`
	~~`double y = m*(double)x + h;`~~
	`y += m;`
	`set_pixel(x, (int)y, color);`
`}`

`//ONLY FOR m > 1`
`int dx = x2 - x1, dy = y2 - y1;`
`double m_inverse = (double)(dy)/(double)(dx); //slope`
~~`double h = y1 - m*x1; //y-intercept`~~
`set_pixel(x1, y1, color); //starting pixel at the origin`
`int y = y1;`
`double x = (double)x1;`
`while(--dy) {`
	`++y;`
	~~`double y = m*(double)x + h;`~~
	`x += m_inverse;`
	`set_pixel((int)x, y, color);`
`}`

`//SWITCHING METHOD (INDEPENDENT)`
`int dx = x2 - x1, dy = y2 - y1;`
`double m = (double)(dy)/(double)(dx); //slope`
`int xstep = (dx > 0) ? 1 : -1;`
`double ystep = (dy > 0) ? m : -m;`
`dx = (dx > 0) ? dx : -dx;`
`set_pixel(x1, y1, color); //starting pixel at the origin`
`int x = x1;`
`double y = (double)y1;`
`while(--dx) {`
	`x += xstep; y += ystep;`
	`set_pixel(x, (int)y, color);`
`}`