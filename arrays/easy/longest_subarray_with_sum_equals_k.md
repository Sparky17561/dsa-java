# Longest Subarray with Sum K (Sliding Window)

## Description
This solution finds the length of the longest subarray that sums to `k` using the **Sliding Window** technique. This approach is highly optimized for space but **only works for arrays with non-negative numbers**.

## Algorithm
1.  **Expand:** Move the `right` pointer to add elements to the `sum`.
2.  **Shrink:** If `sum > k`, move the `left` pointer to remove elements until `sum <= k`.
3.  **Check:** If `sum == k`, update `maxLen` with the current window size (`right - left + 1`).
4.  **Repeat** until `right` reaches the end of the array.

## Constraints
* **Input:** `nums` (Array of integers), `k` (Target sum)
* **Limitation:** The array **must not contain negative numbers**. If negatives are present, the window logic breaks because adding an element doesn't guaranteed increase the sum.

## Complexity
* **Time Complexity:** $O(N)$ - Each element is added and removed at most once.
* **Space Complexity:** $O(1)$ - Only uses a few variables for pointers and sum.

## Java Implementation
```java
class Solution {
    public int longestSubarray(int[] nums, int k) {
        int left = 0;
        int right = 0;
        int maxLen = 0;
        long sum = 0;

        while(right < nums.length){
            sum += nums[right];

            // Shrink window from left if sum is too large
            while(left <= right && sum > k){
                sum -= nums[left];
                left++;                 
            }

            // Update maxLen if we found the target
            if(sum == k){
                maxLen = Math.max(maxLen, right - left + 1);
            }

            right++;
        }
        return maxLen;
    }
}