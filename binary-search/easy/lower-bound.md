
# 📌 Lower Bound (Binary Search)

## 🔹 Problem

Find the **first index** in a sorted array where the value is **greater than or equal to `x`**.

This is called the **lower bound**.

If no such index exists → return `-1`.

---

## 🔹 Example

### Example 1

```
nums = [1, 2, 4, 4, 5]
x = 4
```

Output → `2`
Explanation → First `>= 4` is at index `2`.

---

### Example 2

```
nums = [1, 2, 3]
x = 6
```

Output → `-1`
Explanation → No element ≥ 6.

---

## 🔹 Approach

We use **Binary Search** because the array is sorted.

### Steps

1. Initialize:

   * `left = 0`
   * `right = n - 1`
   * `ans = -1`

2. While `left <= right`

   * Find `mid`
   * If `nums[mid] >= x`

     * Store `mid` as answer
     * Search left side (`right = mid - 1`)
   * Else

     * Search right side (`left = mid + 1`)

3. Return `ans`.

---

## 🔹 Why It Works

When we find a number ≥ x,
there **might be a smaller valid index on the left**,
so we keep searching left.

This ensures we get the **first occurrence**.

---


## 🔹 Code (Java)

```java
class Solution {
    public int lowerBound(int[] nums, int x) {
        int n = nums.length;
        int left = 0;
        int right = n - 1;
        int ans = -1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (nums[mid] >= x) {
                ans = mid;        // possible answer
                right = mid - 1;  // search left
            } else {
                left = mid + 1;   // search right
            }
        }

        return ans;
    }
}
```

---

## 🔹 Time & Space Complexity

| Metric           | Value        |
| ---------------- | ------------ |
| Time Complexity  | **O(log n)** |
| Space Complexity | **O(1)**     |

---

## 🔹 Edge Cases

✔ Empty array
✔ All elements smaller than x
✔ All elements greater than x
✔ Duplicates present

---

## 🔹 Related Problems

* Upper Bound
* First Occurrence of Element
* Last Occurrence of Element
* Search Insert Position (LeetCode)

---

## 🔹 Real World Use

* Finding insertion position in sorted DB index
* Search optimization
* Range queries in search engines
* Version lookup in distributed systems

