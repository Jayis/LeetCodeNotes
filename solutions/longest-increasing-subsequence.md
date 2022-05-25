# Longest Increasing Subsequence

## Solution
I think there are two solutions worth remembering.
- DP - `O(N^2)`
- Greedy with Binary Search - `O(NlogN)`

### DP
DP is quite simple.  
Let `dp[i]` be the length of the longest increasing subsequence that ends at `nums[i]`.  
The recursive equation would then be  
```python
dp[i] = max(*[dp[j] for j in range(i)]) + 1
```
Since we have a for-loop over `dp[i]` (`O(N)`),  
and for each `dp[i]` we have a for-loop over `dp[j]` (`O(N)`),  
we got `O(N^2)`.

### Greedy with Binary Search
The solution is strongly related to `Patient Sort`.  
Please see the reference below.

We can place the `nums[i]` from `0` to `n-1` on several piles.  
And we'll place `nums[i]` on `piles[j]` if a longest increase sequence endswith `nums[i]` and has length of `j`.  

To do this, we'll have to find a number from piles that is smaller than `nums[i]` and has the longest **LIS**, which means the biggest pile index.  
Let's say the index we found was `j`.  
Then the length of **LIS** ends with `nums[i]` will be `j+1`.  
And we'll place `nums[i]` on `piles[j+1]`.  
So each time we decide where to place `nums[i]`, we need to do a binary search on the top elements of piles to find the leftmost pile with top elements bigger than `nums[i]`.

Since we need a binary search over piles[j] (bounded by `O(logN)`) for each number (`O(N)`),  
we got `O(N logN)` time complexity.

We'll need `O(N)` space if we use a array to record the top element of each pile. 

---
## Good Discussions
[[C++/Python] DP, Binary Search, BIT Solutions - Picture explain - O(NlogN)](https://leetcode.com/problems/longest-increasing-subsequence/discuss/1326308/C++Python-DP-Binary-Search-BIT-Solutions-Picture-explain-O(NlogN))
https://leetcode.com/problems/longest-increasing-subsequence/discuss/74824/JavaPython-Binary-search-O(nlogn)-time-with-explanation

---
## Good Materials
[Patient Sort](https://www.cs.princeton.edu/courses/archive/spring13/cos423/lectures/LongestIncreasingSubsequence.pdf) 