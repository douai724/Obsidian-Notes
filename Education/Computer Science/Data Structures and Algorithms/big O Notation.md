### Definition
Big O is a notation used to describe the computational complexity of an algorithm. The computational complexity of an algorithm is split into two parts: time complexity and space complexity. The time complexity of an algorithm is the amount of time the algorithm needs to run relative to the input size. The space complexity of an algorithm is the amount of memory allocated by the algorithm when run relative to the input size.

Complexity is described by a function of variables that can change with the input. The most common variable is n, which usually describes the length of an input array or string. This function is wrapped by a capital O. Here are some example complexities:
- $O(n)$
- $O(n^2)$
- $O(2^n)$
- $O(log\space n)$
- $O(n * m)$

These functions describe how the amount of operations/memory needed by the algorithm grows as the arguments **tend to infinity**. 
Because the variables are tending to infinity, **constants are always ignored**. That means that $O(9999999n)=O(8n)=O(n)=(\frac n 500)$

Being able to analyse an algorithm and derive its time and space complexity is a crucial skill. Interviewers will **almost always** ask you for your algorithm's complexity to check that you actually understand your algorithm and didn't just memorize/copy the code. Being able to analyse an algorithm also enables you to determine what parts of it can be improved.

The best complexity possible is $O(1)$, called "constant time" or "constant space". It means that the algorithm ALWAYS uses the same amount of resources, regardless of the input.

Note that a constant time complexity doesn't necessarily mean that an algorithm is fast $O(500000)=O(1)$, it just means that its runtime is independent of the input size.

#### Logarithmic time

A logarithm is the inverse operation to exponents. The time complexity $log\space n$ is called logarithmic time and is **extremely** fast. A common time complexity is $O(n * log\space n)$, which is fast for most problems and also the time complexity of efficient sorting algorithms.

Typically, the base of the logarithm will be `2`. This means that if your input is size `n`, then the algorithm will perform `x` operations, where $2^x=n$. However, the base of the logarithm [doesn't actually matter](https://stackoverflow.com/questions/1569702/is-big-ologn-log-base-e/1569710#1569710) for big O, since all logarithms are related by a constant factor.

$O(log\space n)$ means that somewhere in your algorithm, the input is being reduced by a percentage at every step

### Analysing space complexity
When you initialize variables like arrays or strings, your algorithm is allocating memory. We never count the space used by the input (it is bad practice to modify the input), and usually don't count the space used by the output (the answer) unless an interviewer asks us to.



