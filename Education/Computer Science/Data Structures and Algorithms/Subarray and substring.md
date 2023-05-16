> As a reminder, a subarray or substring is a contiguous section of [[Arrays]] or [[strings]].

If a problem has explicit constraints such as:

-   Sum greater than or less than `k`
-   Limits on what is contained, such as the maximum of `k` unique elements or no duplicates allowed

And/or asks for:

-   Minimum or maximum length
-   Number of subarrays/substrings
-   Max or minimum sum

Think about a [[Sliding Window]]. Note that not all problems with these characteristics should be solved with a sliding window, and not all sliding window problems have these characteristics. These characteristics should only be used as a general guideline.

If a problem's input is an integer array and you find yourself needing to calculate multiple subarray sums, consider building a [[Prefix sum]].

The size of a subarray between `i` and `j` (inclusive) is `j - i + 1`. This is also the number of subarrays that end at `j`, starting from `i` or later.