# 🔢 Missing Number | Linear Time & Constant Space

## Intuition
The problem asks us to find the single number missing from an array containing `n` distinct numbers taken from the range `[0, n]`.

Since the array indices naturally range from `0` to `n-1`, and the values range from `0` to `n` (with one missing), we can find the missing number by comparing the **Sum of Indices** vs. the **Sum of Values**.

Instead of calculating two large sums separately (which might cause integer overflow in other languages, though less likely here), we can calculate the difference on the fly.

**Key Insight:**
The difference between the "expected" sum of indices and the "actual" sum of values will leave us with the missing number offset.

* We pair every index `i` with the value `nums[i]`.
* The final missing number is simply `Length + (Sum of Indices - Sum of Values)`.

## Approach

1.  Initialize a variable `res = 0`.
2.  Iterate through the array from `i = 0` to `n-1`.
3.  At each step, add the current index `i` and subtract the current value `nums[i]` from `res`.
    * `res += i - nums[i]`
4.  After the loop, add `n` (the length of the array) to `res`.
    * Why add `n`? Because the indices only go up to `n-1`, but the numbers range up to `n`. The index `n` is never added in the loop, so we add it at the end to balance the equation.



### Trace Example
**Input:** `nums = [3, 0, 1]` (Length `n = 3`)
* **Initial:** `res = 0`
* **i=0:** `res += 0 - 3` -> `res = -3`
* **i=1:** `res += 1 - 0` -> `res = -2`
* **i=2:** `res += 2 - 1` -> `res = -1`
* **Final Step:** `res + n` -> `-1 + 3` -> `2`
* **Output:** `2` (Correct!)

---

## Complexity Analysis

* **Time Complexity:** `O(N)`
    * We iterate through the array exactly once.
* **Space Complexity:** `O(1)`
    * We only use a single integer variable `res` for storage.

---

## Java Code

```java
class Solution {
    public int missingNumber(int[] nums) {
        int res = 0;

        // Calculate the difference between indices and values
        for (int i = 0; i < nums.length; i++) {
            res += i - nums[i];
        }

        // Add n (array length) because the loop only covers indices 0 to n-1
        return res + nums.length;
    }
}