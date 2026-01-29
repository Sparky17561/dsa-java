
# 🔁 Check if Array Is Sorted and Rotated

## 📌 Problem Statement

Given an integer array `nums`, return `true` if the array is **sorted in non-decreasing order** and then **rotated some number of times** (possibly zero). Otherwise, return `false`.

🔗 **LeetCode Link:**
[https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/)

---

## 🧠 Intuition

A sorted array, when rotated, can have **at most one point** where the order breaks.

Example:

* Sorted: `[1, 2, 3, 4, 5]`
* Rotated: `[3, 4, 5, 1, 2]` → only **one drop** (`5 > 1`)

If there are **more than one such drop**, the array cannot be sorted and rotated.

---

## ✅ Key Observation

For a valid sorted + rotated array:

* The number of indices `i` where
  `nums[i] > nums[i + 1]`
  should be **≤ 1**
* Since the array is circular, we also compare the **last element with the first**

---

## 🛠️ Approach

1. Traverse the array once.
2. Count how many times `nums[i] > nums[(i + 1) % n]` occurs.
3. If this count exceeds `1`, return `false`.
4. Otherwise, return `true`.

---

## 💡 Java Implementation

```java
class Solution {
    public boolean check(int[] nums) {
        int n = nums.length;
        int check = 0;

        for (int i = 0; i < n; i++) {
            if (nums[i] > nums[(i + 1) % n]) {
                check++;
            }
            if (check > 1) return false;
        }
        return true;
    }
}
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)` — single pass through the array
* **Space Complexity:** `O(1)` — no extra space used

---

## 🧪 Example Walkthrough

### Example 1

```
Input: [3, 4, 5, 1, 2]
Drops: 5 > 1 → 1 drop ✅
Output: true
```

### Example 2

```
Input: [2, 1, 3, 4]
Drops: 2 > 1, 4 > 2 → 2 drops ❌
Output: false
```

---

## 📝 Summary

* A sorted and rotated array can only have **one order violation**
* Circular comparison (`(i + 1) % n`) is the trick
* Clean, optimal, and interview-approved solution 🚀

