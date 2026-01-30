
# 📌 Problem: Rotate Array

Rotate an array by `k` steps **in-place**.

---

## 🚀 Optimal Approach: Reversal Algorithm (Most Important)

### 🧠 Core Idea

Rotation is just **rearranging parts of the array**.
Instead of rotating one-by-one (slow), we **reverse sections** of the array.

---

## 🔁 Right Rotation by `k` Steps

### Steps:

1. **Normalize `k`**

   ```
   k = k % n
   ```
2. **Reverse entire array**
3. **Reverse first `k` elements**
4. **Reverse remaining `n - k` elements**

### Why this works?

* Reversing flips the order
* Reversing sub-parts restores correct relative order

---

### 🧪 Example (Right Rotate)

```
nums = [1,2,3,4,5,6,7], k = 3
```

Steps:

```
Reverse all       → [7,6,5,4,3,2,1]
Reverse first k   → [5,6,7,4,3,2,1]
Reverse rest      → [5,6,7,1,2,3,4]
```

---

## 🔄 Left Rotation by `k` Steps (Concept)

### Steps:

1. Normalize `k`
2. Reverse first `k` elements
3. Reverse remaining `n-k` elements
4. Reverse entire array

---

## ⏱️ Time & Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)` (in-place)

✔ Best possible solution
✔ No extra array used

---

## ⚠️ Exam Notes (Very Important)

* Always do `k = k % n`
* Reversal logic uses **two pointers**
* This approach avoids TLE for large inputs

---

## ✅ Code: Reversal Method (Right Rotation)

```java
class Solution {

    public void reverse(int[] arr, int l, int r) {
        int temp;
        while (l < r) {
            temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            l++;
            r--;
        }
    }

    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;

        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }
}
```

---

# 🔹 Simple Approach: Left Rotate by **1 Position**

### 🧠 Idea

* Save first element
* Shift all elements left
* Put saved element at the end

---

### Steps:

1. Store first element in temp
2. Shift elements left
3. Place temp at last index

---

## ⏱️ Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`
* ⚠️ Repeating this `k` times → `O(n*k)` (not optimal)

---

## ✅ Code: Left Rotate by One

```java
class Solution {
    public void leftRotateByOne(int[] arr) {
        int temp = arr[0];

        for (int i = 1; i < arr.length; i++) {
            arr[i - 1] = arr[i];
        }

        arr[arr.length - 1] = temp;
    }
}
```

---

## 🧠 Quick Recall Summary (Last 10 Seconds)

* **Best solution → Reversal Algorithm**
* Right rotate:

  ```
  reverse(all)
  reverse(0 → k-1)
  reverse(k → n-1)
  ```
* TC: `O(n)` | SC: `O(1)`
* One-by-one rotation = slow ❌

