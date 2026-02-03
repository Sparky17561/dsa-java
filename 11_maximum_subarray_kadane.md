# Maximum Subarray (Kadane's Algorithm)

## Description
Given an integer array `nums`, find the subarray with the largest sum and return its sum. This is a classic dynamic programming problem solved efficiently using **Kadane's Algorithm**.

## Algorithm (Kadane's Algorithm)
The core idea is to maintain a running sum (`currSum`) and reset it whenever it becomes negative, as a negative prefix will only hurt future subarray sums.

1.  **Initialize:**
    * `currSum = 0`: The sum of the current subarray we are building.
    * `maxSum = Integer.MIN_VALUE`: Stores the highest sum found so far.
2.  **Iterate:** Loop through each number `num` in the array:
    * Add `num` to `currSum`.
    * **Update Max:** Check if `currSum` is greater than `maxSum`. If so, update `maxSum`.
    * **Reset Decision:** If `currSum` drops below `0`, it means the current subarray has become a "burden" (negative sum). Reset `currSum` to `0` to start a fresh subarray from the next element.

## Key Edge Case
* **All Negative Numbers:** Because we update `maxSum` *before* resetting `currSum`, this logic correctly handles arrays like `[-5, -2, -9]`. The algorithm will capture `-2` as the maximum before resetting.

## Complexity
* **Time Complexity:** $O(N)$ - We iterate through the array exactly once.
* **Space Complexity:** $O(1)$ - We only use two variables (`currSum`, `maxSum`).

## Java Implementation
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currSum = 0;
        int maxSum = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
            currSum += nums[i];
            
            // Important: Update maxSum BEFORE resetting currSum
            // This ensures we capture the max value even if it's negative.
            maxSum = Math.max(maxSum, currSum);
            
            if (currSum < 0) {
                currSum = 0;
            }
        }
        return maxSum;
    }
}