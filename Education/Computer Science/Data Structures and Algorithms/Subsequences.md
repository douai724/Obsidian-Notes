> A subsequence is a portion of an array/string that keeps the same order but doesn't need to be contiguous.
> 
> For example, subsequences of `[1, 2, 3, 4]` include: `[1, 3]`, `[4]`, `[]`, `[2, 3]`, but not `[3, 2]`, `[5]`, `[4, 1]`.

dynamic programming is used to solve a lot of subsequence problems.

From the patterns we have learned so far, the most common one associated with subsequences is two pointers when two input [[Arrays]]/[[strings]] are given. Because prefix sums and [[Sliding Window]] represent subarrays/substrings, *they are not applicable here*.