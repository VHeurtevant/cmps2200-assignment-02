# CMPS 2200 Assignment 2

**Name:**_________________________

In this assignment we'll work on applying the methods we've learned to analyze recurrences, and also see their behavior
in practice. As with previous
assignments, some of of your answers will go in `main.py` and `test_main.py`. You
should feel free to edit this file with your answers; for handwritten
work please scan your work and submit a PDF titled `assignment-02.pdf`
and push to your github repository.


## Part 1. Asymptotic Analysis

Derive asymptotic upper bounds of work for each recurrence below.

* $W(n)=2W(n/3)+1$

We see at each level, the cost contribution per node is constant,so therefore the cost dominates from the amount of nodes per level and not from the growth/shrinking of n. The amount of nodes per level grows geometrically, with $2^i$ nodes per level- so we will have a leaf dominated recurrence as a result. The cost of the leaves is well known to be $O(n^{\log_{b}a}$, so our bound is $O(n^{\log_{3}(2)}$.
 
* $W(n)=5W(n/4)+n$
We see from the next level, the total cost is $5(n/4) > n$. So this is also a leaf dominated recursion, which means the bound will be $O(n^{\log_{4}(5)})$. 

* $W(n)=7W(n/7)+n$
 We see from the next level, the total cost is $7(n/7) = n$. So this is a balanced recursion, which means the cost will be the number of levels multiplied by cost per level. There is a total of $\log_7(n)$ levels, with a cost of $n$ per level, so the bound will be $O(n\log_7(n)$.

* $W(n)=9W(n/3)+n^2$
  We see from the next level, the total cost is $9(n^2/3^2)=n^2$. So the cost is the same at each level, meaning we have a balanced recursion. The maximum amount of levels is $\log_3(n)$, so we have a bound of $O(n^2\log_3(n)).$
  
* $W(n)=8W(n/2)+n^3$
  We see from the next level, the total cost is $8(n^3/2^3)=n^3$. So the cost is the same at each level, meaning we have a balanced recursion. The maximum amount of levels is $\log_2(n)$, so we have a bound of $O(n^3\log_2(n)).$

* $W(n)=49W(n/25)+n^{3/2}\log n$
We write the cost of the $i$ level as $49^{i}*\frac{n^{3/2}{25^{3i/2}}*(\log(n)-i\log(25)$. Simplifying this, we have $n^{3/2}*\frac{49}{25^3/2}^i (\log(n)-i\log(25).$ Note that the growth/shrink factor, $r=\frac{49}{25^3/2} = \frac{49}{125} < 1$. This implies geometric shrinking, So our cost will be dominated towards the root. Therefore the bound is simply the root, $O(n^{3/2}\log n)$
 
* $W(n)=W(n-1)+2$
  Note that because the subproblem is only decreasing arithmetically rather than geometrically, we have a balanced recursion. The largest level will have a cost of 2,which is constant, and there will be n total levels, so our bound is $O(n)$.
* $W(n)= W(n-1)+n^c$, with $c\geq 1$
Likewise, the cost is balanced here due to no geometric decay/growth of n, so we simply take the cost of $n$ levels and multiply it by the maximum cost. The maximum cost will be the root, $n^c$, so our bound is $O(n^{c+1})$
* $W(n)=W(\sqrt{n})+1$

Because the cost is 1, then the cost per level depends on the nodes per level. To find the max level, we want to solve for the $L$ such that $n^{(1/2)^L} <= 2$.Taking log of both sides, we have $1/2^L \log_2(n) <= 1$ Therefore, $2^L >= log_2(n).$
Taking log of both sides again, we find $L >= log(log(n)).$ So our bound is $O(\log_2 \log_2 (n))$.

## Part 2. Algorithm Comparison

Suppose that for a given task you are choosing between the following three algorithms:

  * Algorithm $\mathcal{A}$ solves problems by dividing them into
      five subproblems of half the size, recursively solving each
      subproblem, and then combining the solutions in linear time.
    
  * Algorithm $\mathcal{B}$ solves problems of size $n$ by
      recursively solving two subproblems of size $n-1$ and then
      combining the solutions in constant time.
    
  * Algorithm $\mathcal{C}$ solves problems of size $n$ by dividing
      them into nine subproblems of size $n/3$, recursively solving
      each subproblem, and then combining the solutions in $O(n^2)$
      time.

    What are the asymptotic running times of each of these algorithms?
    Which algorithm would you choose?


.  
.  
.  
.  
. 
. 



## Part 3: Parenthesis Matching

A common task of compilers is to ensure that parentheses are matched. That is, each open parenthesis is followed at some point by a closed parenthesis. Furthermore, a closed parenthesis can only appear if there is a corresponding open parenthesis before it. So, the following are valid:

- `( ( a ) b )`
- `a () b ( c ( d ) )`

but these are invalid:

- `( ( a )`
- `(a ) ) b (`

Below, we'll solve this problem three different ways, using iterate, scan, and divide and conquer.

**3a. iterative solution** Implement `parens_match_iterative`, a solution to this problem using the `iterate` function. **Hint**: consider using a single counter variable to keep track of whether there are more open or closed parentheses. How can you update this value while iterating from left to right through the input? What must be true of this value at each step for the parentheses to be matched? To complete this, complete the `parens_update` function and the `parens_match_iterative` function. The `parens_update` function will be called in combination with `iterate` inside `parens_match_iterative`. Test your implementation with `test_parens_match_iterative`.


.  
. 



**3b.** What are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

**enter answer here**

.  
. 



**3c. scan solution** Implement `parens_match_scan` a solution to this problem using `scan`. **Hint**: We have given you the function `paren_map` which maps `(` to `1`, `)` to `-1` and everything else to `0`. How can you pass this function to `scan` to solve the problem? You may also find the `min_f` function useful here. Implement `parens_match_scan` and test with `test_parens_match_scan`

.  
. 



**3d.** Assume that any `map`s are done in parallel, and that we use the efficient implementation of `scan` from class. What are the recurrences for the Work and Span of this solution? 

**enter answer here**

.  
.  




**3e. divide and conquer solution** Implement `parens_match_dc_helper`, a divide and conquer solution to the problem. A key observation is that we *cannot* simply solve each subproblem using the above solutions and combine the results. E.g., consider '((()))', which would be split into '(((' and ')))', neither of which is matched. Yet, the whole input is matched. Instead, we'll have to keep track of two numbers: the number of unmatched right parentheses (R), and the number of unmatched left parentheses (L). `parens_match_dc_helper` returns a tuple (R,L). So, if the input is just '(', then `parens_match_dc_helper` returns (0,1), indicating that there is 1 unmatched left parens and 0 unmatched right parens. Analogously, if the input is just ')', then the result should be (1,0). The main difficulty is deciding how to merge the returned values for the two recursive calls. E.g., if (i,j) is the result for the left half of the list, and (k,l) is the output of the right half of the list, how can we compute the proper return value (R,L) using only i,j,k,l? Try a few example inputs to guide your solution, then test with `test_parens_match_dc_helper`.



.  
. 





**3f.** Assuming any recursive calls are done in parallel, what are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

**enter answer here**

.  
. 


 
 


