A prefix sum is a technique that can be used with integer [[Arrays]]. The idea is to create an array `prefix` where `prefix[i]` is the sum of all elements up to the index `i` (inclusive). For example, given `nums = [5, 2, 1, 6, 3, 8]`, we would have `prefix = [5, 7, 8, 14, 17, 25]`.

Prefix sums allow us to find the sum of any [[Subarray and substring]] in $O(1)$. If we want the sum of the subarray from `i` to `j` (inclusive), then the answer is `prefix[j] - prefix[i - 1]`, or `prefix[j] - prefix[i] + nums[i]` if you don't want to deal with the out of bounds case when `i = 0`.

Building a prefix sum is very simple. Here's some pseudocode:

	Given an integer array nums,
	prefix = [nums[0]]
	for i in [1, len(nums) - 1]:
	    prefix.append(nums[i] + prefix[prefix.length - 1])

Initially, we start with just the first element. Then we iterate with `i` starting from index `1`. At any given point, the last element of `prefix` will represent the sum of all the elements in the input up to but not including index `i`. So we can add that value plus the current value to the end of `prefix` and continue to the next element.

A prefix sum is a great tool whenever a problem involves sums of a subarray. It only costs $O(n)$ to build but allows all future subarray queries to be $O(1)$, so it can usually improve an algorithm's time complexity by a factor of $O(n)$, where n is the length of the array.

**Example:** Given an integer array `nums`, an array `queries` where `queries[i] = [x, y]` and an integer `limit`, return a boolean array that represents the answer to each query. A query is `true` if the sum of the subarray from `x` to `y` is less than `limit`, or `false` otherwise.

For example, given `nums = [1, 6, 3, 2, 7, 2]` and `queries = [[0, 3], [2, 5], [2, 4]]` and `limit = 13`, the answer is `[true, false, true]`. For each query, the subarray sums are `[12, 14, 12]`.

	public boolean[] answerQueries(int[] nums,int[][] queries,int limit){
	    int[] prefix = new int[nums.length];
	    prefix[0] = nums[0];
	    for (int i = 1; i < nums.length; i++) {
		    prefix[i] = prefix[i - 1] + nums[i];
		}
	    boolean[] ans = new boolean[queries.length];
	    for (int i = 0; i < queries.length; i++) {
		    int x = queries[i][0], y = queries[i][1];
		    int curr = prefix[y] - prefix[x] + nums[x];
		    ans[i] = curr < limit;
	    }
    return ans;
	}



