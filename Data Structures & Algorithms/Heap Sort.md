
## [[Heap Sort Code]]
## Step 1

### Layout the array with i as the starting index iterating to the last index into a [[Binary Tree]]. There isn't a function of making the tree since the tree remembers the indexes of the array.

![[ezgif.com-video-to-gif-converter (2).gif|444]]

## Step 2

### Heapify the tree by moving each branches highest node up the tree. A Max Heap is where the root is larger than its children


### Execute (i-1)/2 for the children of each branch and swap the child and parent if the child is bigger. 



![[ezgif.com-video-to-gif-converter (3).gif|492]]

## Step 3

### Swap the first and last indexes to get the bigger node to the last index

![[ezgif.com-video-to-gif-converter (4).gif|478]]

## Step 4

### Repeat step 2 and 3 until (i-1)/2 and i are at the same index which means the highest node should be the lowest number and therefore the array is sorted.

![[ezgif.com-video-to-gif-converter (5).gif|436]]