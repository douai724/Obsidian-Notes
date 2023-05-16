
**Two-pointers** is an extremely common technique used to solve *array and string problems*. It involves having two integer variables that both move along an iterable. In this article, we are focusing on arrays and strings. This means we will have two integers, usually named something like `i` and `j`, or `left` and `right` which each represent an index of the array or string.

There are several ways to implement two-pointers. To start, let's look at the following method:

> Start the pointers at the edges of the input. Move them towards each other until they meet.

**Converting this idea into instructions:**

1.  Start one pointer at the *first index* `0` and the other pointer at the last index `input.length - 1`.
2.  Use a *while loop* until the pointers are *equal* to each other.
3.  At *each iteration of the loop, move the pointers towards each other*. This means either increment the pointer that started at the first index, decrement the pointer that started at the last index, or both. Deciding which pointers to move will depend on the problem we are trying to solve.

**Here's some pseudocode illustrating the concept:**

	function fn(arr):
	    left = 0
	    right = arr.length - 1
	    while left < right:
		    Do some logic here depending on the problem
		    Do some more logic here to decide on one of the following:
		        1. left++
		        2. right--
		        3. Both left++ and right--

The strength of this technique is that we will never have more than  iterations for the while loop. Therefore, if we can keep the work inside each iteration at �(1)O(1), this technique will result in a linear runtime. Let's look at some examples.

---

> **Example 1**: Return `true` if a given string is a palindrome, `false` otherwise.
> 
> A string is a palindrome if it reads the same forwards as backwards. That means, after reversing it, it is still the same string. For example: "abcdcba", or "racecar".

After reversing a string, the *first* character becomes the *last* character. If a string is the same after being reversed, *that means the first character is the same as the last character*, the second character is the same as the second last character, and so on. We can use the two pointers technique here to check that all corresponding characters are equal. To start, we check the first and last character using two separate pointers. To check the next pair of characters, we just need to move our pointers towards each other one position. *We continue until the pointers meet each other or we find a mismatch*.
`n` is the total number of characters, so `n - i - 1` corresponds to the last, second last, third last etc. character. The `-1` is necessary since the inputs are 0-indexed.

	public boolean checkIfPalindrome(String s) {
	    int left = 0;
	    int right = s.length() - 1;
	    while (left < right) {
		    if (s.charAt(left) != s.charAt(right)) {
				return false;
		    }
	    left++;
	    right--;
	    }
	    return true;
	}

Notice that if the input was an array of characters instead of a string, the algorithm wouldn't change. The two-pointers technique works as long as the index variables are moving along some abstract iterable.

This algorithm is very efficient as not only does it run in $O(n)$, but it also uses only $O(1)$ space. No matter how big the input is, we always only use two integer variables.

---

> **Example 2**: Given a **sorted** array of unique integers and a target integer, return `true` if there exists a pair of numbers that sum to target, `false` otherwise. This problem is similar to [Two Sum](https://leetcode.com/problems/two-sum/).
> 
> For example, given `nums = [1, 2, 4, 6, 8, 9, 14, 15]` and `target = 13`, return true because `4 + 9 = 13`.

### Brute Force Solution
The brute force solution would be to iterate over all pairs of integers. Each number in the array can be paired with another number, so this would result in a time complexity of $O(n^2)$, where n is the length of the array. Because the array is sorted, we can use two pointers to improve to an $O(n)$ time complexity.

### Two-pointer Solution
Let's use the example input. With two pointers, we start by looking at the first and last number. Their sum is `1 + 15 = 16`. Because `16 > target`, we need to make our current sum smaller. Therefore, we should move the `right` pointer. Now, we have `1 + 14 = 15`. Again, move the right pointer because the sum is too large. Now, `1 + 9 = 10`. Since the sum is too small, we need to make it bigger, which can be done by moving the `left` pointer. `2 + 9 = 11 < target`, so move it again. Finally, `4 + 9 = 13 = target`

**The reason this algorithm works**: because the numbers are sorted, moving the left pointer permanently increases the value the left pointer points to (`nums[left] = x`). Similarly, moving the right pointer permanently decreases the value the right pointer points to (`nums[right] = y`). If we have `x + y > target`, then we can never have a solution with `y` because `x` can only increase. So if a solution exists, we can only find it by decreasing `y`. The same logic can be applied to `x` if `x + y < target`.

	public boolean checkForTarget(int[] nums, int target) {
	    int left = 0;
	    int right = nums.length - 1;
		while (left < right) {
		    int curr = nums[left] + nums[right];
		    if (curr == target) {
				return true;
		    }
		    if (curr > target) {
		        right--;
		    } else {
		        left++;
		    }
	    }
    return false;
	}

### Closing notes

Remember that the methods laid out here are just guidelines. For example, in the first method, we started the pointers at the first and last index, but sometimes you might find a problem that involves starting the pointers at different indices. In the second method, we moved two pointers forward along two different inputs. Sometimes, there will only be one input array/string, but we still initialize both pointers at the first index and move both of them forward.

Two pointers just refers to using two integer variables to move along some iterables. The strategies we looked at in this article are the most common patterns, but always be on the lookout for a different way to approach a problem.