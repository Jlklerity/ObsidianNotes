	
	total = 0
	for i = 1 to n
	  for j = 1 to n
	   total = total + (i * j)

| **Line of Code**          | **Calculation**                                | **Total Steps** |
| ------------------------- | ---------------------------------------------- | --------------- |
| `total = 0`               | 1                                              | $1$             |
| `for i = 1 to n`          | $(n + 1)$ checks + $n$ increments              | $2n + 1$        |
| `for j = 1 to n`          | $n \times ((n + 1)$ checks + $n$ increments$)$ | $2n^2 + n$      |
| `total = total + (i * j)` | 3 steps $\times n^2$ executions                | $3n^2$          |

-----

	  sum = 0
	  for i = 1 to n
	      for j = 1 to n
	          if i == j
	              sum = sum + mat[i][j]

|**Line of Code**|**Calculation**|**Total Steps**|
|---|---|---|
|`1 sum = 0`|1 step|$1$|
|`2 for i = 1 to n`|$(n + 1)$ checks + $n$ increments|$2n + 1$|
|`3 for j = 1 to n`|$n \times ((n + 1)$ checks + $n$ increments$)$|$2n^2 + n$|
|`4 if i == j`|1 step $\times n^2$ executions|$n^2$|
|`5 sum = sum + mat[i][j]`|3 steps $\times n$ executions|$3n$|

------

	 total = 0
	for i = 1 to n
	      for j = 1 to i
	          total = total + ar[j]

|**Line of Code**|**Calculation**|**Total Steps**|
|---|---|---|
|`1 total = 0`|1 step|$1$|
|`2 for i = 1 to n`|$(n + 1)$ checks + $n$ increments|$2n + 1$|
|`3 for j = 1 to i`|Summing $(i + 1)$ checks + $i$ increments for $i=1$ to $n$|$n^2 + 2n$|
|`4 total = total + ar[j]`|3 steps $\times$ sum of $1$ to $n$ executions|$\frac{3n(n+1)}{2}$|
