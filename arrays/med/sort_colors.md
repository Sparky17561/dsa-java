
# 📌 Problem: Sort Colors (0s, 1s, 2s)

You are given an array containing only `0`, `1`, and `2`.
Sort the array **in-place** without using extra space.

---

## 🧠 Core Idea (Dutch National Flag Algorithm)

We divide the array into **four regions** using three pointers:

```
[ 0s | 1s | unknown | 2s ]
   ^     ^         ^
  low   mid       high
```

* `low` → boundary for **0s**
* `mid` → current element being checked
* `high` → boundary for **2s**

---

## 🚀 Algorithm Steps

1. Initialize:

   ```
   low = 0, mid = 0, high = n - 1
   ```
2. While `mid <= high`:

   * If `nums[mid] == 0`

     * Swap with `low`
     * `low++`, `mid++`
   * If `nums[mid] == 2`

     * Swap with `high`
     * `high--`
     * ❌ do NOT increment `mid`
   * If `nums[mid] == 1`

     * Just `mid++`

---

## ⚠️ Important Rules (Very Exam-Important)

* Use `while (mid <= high)`
* After swapping with `high`, **re-check `mid`**
* After swapping with `low`, it’s safe to move both pointers

---

## 🧪 Example Dry Run

Input:

```
[2,0,2,1,1,0]
```

Process:

```
[0,0,1,1,2,2]
```

Sorted in one pass ✔

---

## ⏱️ Time & Space Complexity

* **Time Complexity:** `O(n)` (single traversal)
* **Space Complexity:** `O(1)` (in-place)
* **Stable:** ❌ No
* **Sorting Method:** Partition-based

---

## ❌ Common Mistakes

* Using `mid < high` instead of `mid <= high`
* Incrementing `mid` after swapping with `high`
* Using extra arrays (not allowed)

---

## 🧠 One-Line Interview Explanation

> “I use the Dutch National Flag algorithm with three pointers to partition 0s, 1s, and 2s in one pass.”

---

## ✅ Final Code (Correct & Clean)

```java
class Solution {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;
        int temp;

        while (mid <= high) {
            if (nums[mid] == 0) {
                temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            } 
            else if (nums[mid] == 2) {
                temp = nums[high];
                nums[high] = nums[mid];
                nums[mid] = temp;
                high--;
            } 
            else {
                mid++;
            }
        }
    }
}
```

---

## 🧠 10-Second Recall Trick

* 0 → left
* 2 → right
* 1 → middle
* Swap with `high` → **don’t move `mid`**

