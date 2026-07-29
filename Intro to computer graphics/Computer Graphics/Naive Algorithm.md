

![[Pasted image 20260722144019.png]]

`double m = (double)(y2 - y1)/(double)(x2 - x1); //slope
`double h = y1 - m*x1; //y-intercept`
`set_pixel(x1, y1, color); //starting pixel at the origin`
`for(int x = x1 + 1; x < x2; ++x) {`
	`double y = m*(double)x + h;`
	`set_pixel(x, (int)y, color);`
`}`

`//IMPROVED VERSION`
`int dx = x2 - x1, dy = y2 - y1;`
`double m = (double)(dy)/(double)(dx); //slope`
`double h = y1 - m*x1; //y-intercept`
`set_pixel(x1, y1, color); //starting pixel at the origin`
`int x = x1;`
`while(--dx) {`
	`++x;`
	`double y = m*(double)x + h;`
	`set_pixel(x, (int)y, color);`
`}`
