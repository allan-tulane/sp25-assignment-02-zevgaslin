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
.  
.  2^i nodes per level
  cost of each node is 1
  cost of each level is 2^i*1, which is bigger than 1, so leaf dominated
  number of levels:
  n/3^i = 1
  log_3(n)=i
  2^log_3(n) = number of levels
  1 work per level, so W(n) = 2^log_3(n) = n^log_3(2)
  

* $W(n)=5W(n/4)+n$
i = log_4(n)
5^i = nodes in tree = 5^log_4(n)
each node does n work, so k*n work in total
#nodes * w = 5^log_4(n) =n^log_4(5)


* $W(n)=7W(n/7)+n$
Ballenced
i = log_7(n).= num levels
each levle does n work, so w = n*log_7(n) 

* $W(n)=9W(n/3)+n^2$

9(n/3)^2 = 9n^2/9 = n^2 which is the same as the work per level, so balanced. 

n/3^i = 1 -> i = log_3(n)

W(n) = num levels * work per level = n^2log_3(n)

* $W(n)=8W(n/2)+n^3$
* 8*n^3/2^8 = 8n^3/8 = n^3 so balanced
* i = log_2(n)
* w(n) = n^3log_2(n)


* $W(n)=49W(n/25)+n^{3/2}\log n$
* 49*(n^3/2*logn)/(25^(3/2)*logn)
* 49*n^(3/2)/125
* 0.329*n^3/2 decreasing so root dominated
* 
* W(n) = n^3/2log(n)
* 

* $W(n)=W(n-1)+2$
* W(n) = W(n-i) +2*i
* base case when i = n so w(n) = 0
* W(n) = W(n-n) + 2*n = w(0) + 2n = c + 2n
* w(n) = 2n = O(n)



* $W(n)= W(n-1)+n^c$, with $c\geq 1$
* W(n-1) = W(n-2) + (n-1)^c
....
  W(n) = W(n-i) + (n-i+1)^c + (n-i+2)^c ... n^c

Base case assume i=n

W(n) = W(n-n) + Sum from {j = 0 to j = n-1} of (n-j)^c
W(N) = W(0) + n^c+1 = n^c+1


* $W(n)=W(\sqrt{n})+1$

W(n) = W(n^(1/2)^i)+ i

base case n = 2

n^(1/2)^i = 2
(1/2)^ilog_2(n) = 1
2^i = log_2(n)
i = log_2(log_2(n))

leave dominated so W(n) = log_2(log_2(n))



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
    
A: W(n) = 5(n/2) + o(1)
n/2^i = 1 -> i = log_2(n)
5^i = # nodes per level, at bottom level 5^i = 5^log_2(n) = n^log_2(5) = W(n)


B: W(n) = w(n-1) + O(1)
W(n) = 2^iW(n-i) + 2^iO(1) becase you add the w(n-i) + O(1) for each node per level, and the numebr of nodes per level is 2^i

base case: for i=n
W(n) = 2^iW(n-n) + 2^iO(1) = 2^i = 2^n

C: W(n) = 9W(n/3) + o(n^2)
9n^2/9 = n^2 so ballanced

n/3^i = 1 -> i = log_3(n)

W(n) = n^2 * log_3(n)


so C is the least work



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
W(n) = W(n-1) + O(1) = O(n)

S(n) = S(n-1) + O(1) = O(n)

**3c. scan solution** Implement `parens_match_scan` a solution to this problem using `scan`. **Hint**: We have given you the function `paren_map` which maps `(` to `1`, `)` to `-1` and everything else to `0`. How can you pass this function to `scan` to solve the problem? You may also find the `min_f` function useful here. Implement `parens_match_scan` and test with `test_parens_match_scan`

.  
. 



**3d.** Assume that any `map`s are done in parallel, and that we use the efficient implementation of `scan` from class. What are the recurrences for the Work and Span of this solution? 

**enter answer here**
map: W(n) = O(n) S(n) = O(1) bc parallel
scan: W(n) = O(n) S(n) = (log(n))
reduce: W(n) = O(n) S(n) = O(log(n))

total = add them together => W(n) = O(n) S(n) = O(log(n))



**3e. divide and conquer solution** Implement `parens_match_dc_helper`, a divide and conquer solution to the problem. A key observation is that we *cannot* simply solve each subproblem using the above solutions and combine the results. E.g., consider '((()))', which would be split into '(((' and ')))', neither of which is matched. Yet, the whole input is matched. Instead, we'll have to keep track of two numbers: the number of unmatched right parentheses (R), and the number of unmatched left parentheses (L). `parens_match_dc_helper` returns a tuple (R,L). So, if the input is just '(', then `parens_match_dc_helper` returns (0,1), indicating that there is 1 unmatched left parens and 0 unmatched right parens. Analogously, if the input is just ')', then the result should be (1,0). The main difficulty is deciding how to merge the returned values for the two recursive calls. E.g., if (i,j) is the result for the left half of the list, and (k,l) is the output of the right half of the list, how can we compute the proper return value (R,L) using only i,j,k,l? Try a few example inputs to guide your solution, then test with `test_parens_match_dc_helper`.



**3f.** Assuming any recursive calls are done in parallel, what are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

**enter answer here**

W(n) = 2W(n/2) +O(1)
leaf dominated so W(n) = 2^i = 2^log_2(n) = n^log_2(2) = n

S(n) = S(n/2) + O(1)
leaf dominated so i = log_2(n)