---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - algorithms
  - programming
note type: Informational Note
---
- **Dynamic programming** is used to optimise a particular characteristic with defined limits. 
- For instance, in the problem of a bag it is necessary to maximise the cost of elected items with defined limits of a volume of a bag 
- Dynamic programming only works when the problem can be divided into small independent blocks 

The proper way of using Dynamic programming: 
- In every solution of this method it is necessary to create a table 
- Values of cells of the table usually match the characteristic which we are optimising. For our example problem: values were the total cost of items. 
- Every cell represents a subtask, it is necessary to think of how to divide the main problem into small subtasks, in order to define axises. 

> [!info] There is no single formula of resolving problems with dynamic programming 
- You need to tweak the algorithm regarding a particular problem 

The example of the table: 
![[IMG_1615.jpeg]]

And the table for the algorithm of finding the largest common subsequence: 
![[IMG_1616.jpeg]]



