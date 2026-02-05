# 1️⃣ Max Consecutive Ones | Linear Scan

## Intuition
The problem asks us to find the maximum number of consecutive `1`s in a binary array.

This can be solved with a simple **Linear Scan** (one pass) through the array. We maintain a running count of the current streak of ones. Whenever the streak is broken (we encounter a `0`) or the array ends, we compare the current streak against our global maximum.

## Approach

1.  **Initialize Variables:**
    * `count`: Tracks the current streak of consecutive 1s.
    * `res`: Tracks the maximum streak found so far.

2.  **Iterate through the array:**
    * **If `nums[i] == 1`:** Increment the `count`.
    * **If `nums[i] == 0`:** The streak is broken.
        * Update `res` with the maximum of `res` and `count`.
        * Reset `count` to `0`.

3.  **Final Check:**
    * After the loop finishes, we must perform one last `Math.max(res, count)`. This is critical for cases where the array *ends* with a streak of 1s (e.g., `[0, 1, 1]`), as the loop condition won't trigger the "streak broken" logic for that final segment.



---

## Complexity Analysis

* **Time Complexity:** `O(N)`
    * We iterate through the array exactly once.
* **Space Complexity:** `O(1)`
    * We only use two variables (`count` and `res`) for storage.

---

## Java Code

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int res = 0; // Initialize to 0, as streaks cannot be negative
        int count = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 1) {
                // Streak broken: Update max and reset count
                res = Math.max(res, count);
                count = 0;
            } else {
                // Continue streak
                count++;
            }
        }

        // Final check for a streak ending at the last element
        res = Math.max(res, count);

        return res;
    }
}