# 0️⃣ Move Zeroes | Two Pointers (Shift & Fill)

## Intuition
The problem asks us to move all `0`s to the end of an array while maintaining the relative order of the non-zero elements. We must do this **in-place** (without making a copy of the array).

We can solve this using a **Two-Pointer Approach**:
1.  **`left` (Writer):** Keeps track of the position where the next non-zero element *should* go.
2.  **`right` (Reader):** Scans the array to find non-zero elements.



## Approach

This solution operates in two distinct phases:

### Phase 1: Shift Non-Zeros Forward
We iterate through the array with the `right` pointer.
* Whenever we find a **non-zero** number (`nums[right] != 0`), we copy it to the `nums[left]` position.
* We then increment `left`.
* *Result:* All non-zero numbers are now packed at the start of the array. The end of the array still contains "garbage" (duplicate values) that we haven't overwritten yet.

### Phase 2: Fill Remaining Zeros
After the loop finishes, the `left` pointer is sitting at the index immediately after the last non-zero number.
* We run a second loop from `left` to the end of the array.
* We set every element in this range to `0`.

### Trace Example
**Input:** `[0, 1, 0, 3, 12]`

1.  **Shift Phase:**
    * Found `1`: Write to index 0. Array: `[1, 1, 0, 3, 12]`. `left` becomes 1.
    * Found `3`: Write to index 1. Array: `[1, 3, 0, 3, 12]`. `left` becomes 2.
    * Found `12`: Write to index 2. Array: `[1, 3, 12, 3, 12]`. `left` becomes 3.
2.  **Fill Phase:**
    * Fill `0` from index `3` to end.
    * Index 3 becomes `0`.
    * Index 4 becomes `0`.
3.  **Result:** `[1, 3, 12, 0, 0]`

---

## Complexity Analysis

* **Time Complexity:** `O(N)`
    * We traverse the array once to move non-zeros, and potentially once more to fill zeros. Total operations are proportional to `N`.
* **Space Complexity:** `O(1)`
    * We modify the array in-place using only two integer pointers.

---

## Java Code

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int left = 0;

        // Phase 1: Move all non-zero integers to the front
        for (int right = 0; right < nums.length; right++) {
            if (nums[right] != 0) {
                nums[left] = nums[right];
                left++;
            }
        }

        // Phase 2: Fill the remaining positions with zeros
        while (left < nums.length) {
            nums[left] = 0;
            left++;
        }
    }
}