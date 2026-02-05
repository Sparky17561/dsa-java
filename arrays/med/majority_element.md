# 👑 Majority Element | Sorting & Counting

## Intuition
The "Majority Element" is defined as the element that appears more than `n / 2` times.

If we **sort** the array, identical elements will be grouped together. This transforms the problem from "finding the most frequent element" to simply "finding a contiguous segment of duplicates that is long enough."

## Approach

1.  **Sort the Array:** We use `Arrays.sort(nums)`. This brings all duplicate values next to each other.
2.  **Linear Scan:** We iterate through the sorted array and count consecutive identical elements.
    * If `nums[i]` is the same as `nums[i-1]`, we increment the `count`.
    * If `nums[i]` is different, we reset `count` to 1.
3.  **Threshold Check:** As soon as `count` exceeds `n / 2`, we know we found the majority element and return it immediately.



### Optimization Note (The "Middle Index" Trick)
Since the majority element appears more than `n / 2` times, it is mathematically guaranteed to occupy the **middle index** (`nums[n/2]`) of a sorted array.
* *Example:* In `[1, 1, 1, 2, 2]`, the 1s must cross the center.
* While the code below uses a loop to count, you could technically just `return nums[nums.length / 2];` after sorting!

---

## Complexity Analysis

* **Time Complexity:** $O(N \log N)$
    * Sorting the array dominates the time complexity. The linear scan afterwards is just $O(N)$.
* **Space Complexity:** $O(1)$ (or $O(\log N)$)
    * We sort the array in-place (depending on the language's sort implementation, Java uses a variant of QuickSort which uses stack space). We use constant extra space for variables.

---

## Java Code

```java
class Solution {
    public int majorityElement(int[] nums) {
        // Base case: arrays of size 1
        if (nums.length == 1) return nums[0];

        int upperBound = nums.length / 2;
        Arrays.sort(nums); // Group duplicates together
        
        int count = 1;

        for (int i = 1; i < nums.length; i++) {
            // If current matches previous, increment streak
            if (nums[i-1] == nums[i]) {
                count++;
            } else {
                // New number encountered, reset streak
                count = 1;
            }

            // Check if this streak is the majority
            if (count > upperBound) {
                return nums[i];
            }
        }
        
        return nums[0];
    }
}