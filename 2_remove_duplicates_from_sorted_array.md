
## 📌 Problem: Remove Duplicates from Sorted Array

### 🧠 Key Idea (1-liner)

Since the array is **sorted**, all duplicates are **next to each other**.
We keep **one pointer for unique elements** and another to scan the array.

---

## 🚀 Approach: Two Pointers

* `i` → points to the **last unique element index**
* `j` → scans the array from left to right

### How it works:

1. Start `i = 0` (first element is always unique)
2. Loop `j` from index `1` to end
3. If `nums[j] != nums[i]`

   * increment `i`
   * copy `nums[j]` to `nums[i]`
4. After loop, `i + 1` = number of unique elements

👉 **All unique elements are stored from index `0` to `i`**

---

## 🧪 Example

Input:

```
nums = [1,1,2,2,3]
```

Process:

```
Unique part becomes: [1,2,3,_,_]
```

Output:

```
return 3
```

---

## ⏱️ Time & Space Complexity

* **Time Complexity (TC):** `O(n)`
  (single pass through array)

* **Space Complexity (SC):** `O(1)`
  (no extra space, in-place modification)

---

## ⚠️ Important Notes (Exam Gold ✨)

* Works **only because array is sorted**
* No new array created
* Order of unique elements is preserved
* `return i + 1`, not `i`

---

## ✅ Final Code (Revision Ready)

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;

        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```

