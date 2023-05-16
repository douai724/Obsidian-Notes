> Like [[Two Pointers]], sliding windows work the same with [[Arrays and Strings]] - the important thing is that they're iterable with ordered elements. For the sake of brevity, the first part of this article up until the examples will be focusing on [[Arrays]]. However, all the logic is identical for [[strings]]. You can swap every instance of the word "array" with "string" and it will make sense.

Sliding window is another common approach to solving problems related to arrays. A sliding window is actually implemented using two pointers! First, let's start by looking at the concept of a **subarray**. Given an array, [[Subarray and substring]] are just a section of the array. The elements need to be contiguous and in order. For example, with the array `[1, 2, 3, 4]`, the subarrays (grouped by length) are:

-   `[1]`, `[2]`, `[3]`, `[4]`
-   `[1, 2]`, `[2, 3]`, `[3, 4]`
-   `[1, 2, 3]`, `[2, 3, 4]`
-   `[1, 2, 3, 4]`

**A subarray can be defined by two indices, the start and end**. For example, with `[1, 2, 3, 4]`, the subarray `[2, 3]` has a starting index of `1` and an ending index of `2`. Let's call the starting index the **left bound** and the ending index the **right bound**. Another name for subarray in this context is "window", which we will use from now on.

***The idea behind the sliding window technique is to efficiently find the "best" window that fits some constraint.*** Usually, the problem description will define what makes a window "better" (shorter length, larger sum etc.) and the constraint. Imagine that a problem wanted **the length of the longest subarray with a sum less than or equal to k** for an array with positive numbers. In this case, the constraint is `sum(window) <= k`, and the longer the window, the better it is. The general algorithm behind sliding window is:

1.  Define a pointer for the left and right bound that represents the current window, usually both of them starting at `0`.
2.  Iterate over the array with the right bound to "add" elements to the window.
3.  Whenever the constraint is broken, in this example if the sum of the window exceeds `k`, then "remove" elements from the window by incrementing the left bound until the condition is satisfied again.

Here's some pseudocode illustrating the concept:

	function fn(arr):
    left = 0
    for right in [0, arr.length - 1]:
        Do some logic to "add" element at arr[right] to window

        while left < right AND condition from problem not met:
            Do some logic to "remove" element at arr[left] from window
            left++

        Do some logic to update the answer

With our "sum less than `k`" example, we can use a variable `curr` that keeps track of the current sum of the window. That way, we know when the sum exceeds `k` without needing to calculate the window sum from scratch every iteration. We can "add" elements by doing `curr += arr[right]` and "remove" elements by doing `curr -= arr[left]`. The data and logic needed to maintain information about a window will vary between problems.

>You may be thinking: there is a while loop inside of the for loop, isn't the time complexity $O(n^2)$? The reason it is still $O(n)$ is that the while loop can only iterate n times in total for the entire algorithm (`left` starts at `0`, only increases, and never exceeds `n`). If the while loop were to run `n` times on one iteration of the for loop, that would mean it wouldn't run at all for all the other iterations of the for loop. This is what we refer to as [[amortised analysis]] - *even though the **worst case** for an iteration inside the for loop is $O(n)$, it averages out to $O(1)$ when you consider the **entire runtime** of the algorithm.*

> Example 1: Given an array of positive integers `nums` and an integer `k`, find the length of the longest subarray whose sum is less than or equal to `k`.

Let's use an integer `curr` that tracks the sum of the current window. Since the problem wants subarrays whose sum is less than or equal to `k`, we want to maintain `curr <= k`. Let's look at an example where `nums = [3, 1, 2, 7, 4, 2, 1, 1, 5]` and `k = 8`.

The window starts empty, but we can grow it to `[3, 1, 2]` while maintaining the constraint. However, after adding the `7`, the window's sum becomes too large. We need to tighten the window until the sum is below `8` again, which doesn't happen until our window looks like `[7]`. When we try to add the next element, our window again becomes too large, and we need to remove the `7` which means we have `[4]`. We can now grow the window until it looks like `[4, 2, 1, 1]`, but adding the next element makes the sum too large. We remove elements from the left until it fits the constraint again, which happens at `[1, 1, 5]`. The longest subarray we found was `[4, 2, 1, 1]` which means the answer is `4`.

When we add an element to the window by moving the right bound, we just do `curr += value`. When we remove an element from the window by moving the left bound, we just do `curr -= value`. We should remove elements so long as `curr > k`.

	public int findLength(int[] nums, int k) {
	    int left = 0;
	    int curr = 0;
	    int ans = 0;
	    for (int right = 0; right < nums.length; right++) {
	        curr += nums[right];
	        while (curr > k) {
	        curr -= nums[left];
	        left++;
	    }
	    ans = Math.max(ans, right - left + 1);
	}
	    return ans;
	}

Given a subarray **starting** at `left` and ending at `right`, the **length** is `right - left + 1`. As mentioned before, this algorithm has a time complexity of $O(n)$ since all work done inside the for loop is $O(1)$, where n is the length of `nums`. The space complexity is constant because we are only using 3 integer variables. $O(1)$

### Fixed window size
In the examples we looked at above, our window size was variable. We tried to expand it as much as we could while keeping the window within some constraint, and removed elements from the left when it violated the constraint. Sometimes, a problem will specify a **fixed** subarray length. These questions are easy because the criteria are usually the same - just make sure the window size remains the same. To build the initial window (from index `0` to `k - 1`), you can either build it outside of the main loop or you can factor the logic inside your main loop to only consider the window for the answer once it reaches size `k`. Here's some pseudocode for both methods:

	// first approach
	function fn(arr, k):
	    curr = some data type to track the window
	    // build the first window
	    for i in [0, k - 1]:
	        Do something with curr or other variables to build first window
		ans = answer variable, might be equal to curr here depending on the problem
	for i in [k, arr.length - 1]:
	    Add arr[i] to window
	    Remove arr[i - k] from window
	    Update ans
		return ans
	// second approach
	function fn(arr, k):
	    curr = some data type to track the window
	    ans = answer variable
	    for i in range(len(arr)):
		    if i >= k:
		        Update ans
		        Remove arr[i - k] from window
			Add arr[i] to window
	    Update ans    
	    return ans 
		    // Alternatively, you could do something like return 
		    max(ans, curr) if the problem is asking for a maximum value 
		    and curr is tracking that.


