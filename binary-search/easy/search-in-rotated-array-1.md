
# 📘 README — Search in Rotated Sorted Array (Binary Search)

## ✅ Problem

Given a **rotated sorted array**, find the index of a `target` value.

If not found → return `-1`.

Example:

```text
nums = [4,5,6,7,0,1,2]
target = 0
Output = 4
```

---

## ✅ Key Observation

In a rotated sorted array:

👉 The whole array is **not sorted**
👉 But **one half is always sorted**

At any index `mid`:

* Either **left side** is sorted
* Or **right side** is sorted

This property allows binary search to still work.

---

## ✅ Why Binary Search Still Works

Normal Binary Search needs a fully sorted array.

Here we adapt it:

1. Find middle element.
2. Identify which half is sorted.
3. Check if target lies inside that sorted half.
4. If yes → search there.
5. Else → search other half.

So instead of scanning the whole array, we cut search space in half every step.

👉 Time stays **O(log n)**.

---

## ✅ Step-by-Step Algorithm

1️⃣ Start with `low = 0`, `high = n-1`.

2️⃣ Find middle.

3️⃣ If `nums[mid] == target` → return index.

4️⃣ Check which side is sorted:

### Case 1️⃣ Left Half Sorted

```text
nums[low] <= nums[mid]
```

If target in range:

```text
nums[low] <= target < nums[mid]
```

→ search left

Else → search right.

---

### Case 2️⃣ Right Half Sorted

```text
nums[mid] <= nums[high]
```

If target in range:

```text
nums[mid] < target <= nums[high]
```

→ search right

Else → search left.

---

Repeat until found or search space empty.

---

## ✅ Code (Java)

```java
class Solution {

    public int search(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target)
                return mid;

            // LEFT HALF SORTED
            if (nums[low] <= nums[mid]) {

                if (nums[low] <= target && target < nums[mid])
                    high = mid - 1;
                else
                    low = mid + 1;
            }

            // RIGHT HALF SORTED
            else {

                if (nums[mid] < target && target <= nums[high])
                    low = mid + 1;
                else
                    high = mid - 1;
            }
        }

        return -1;
    }
}
```

---

## ✅ Example Walkthrough

```text
nums = [4,5,6,7,0,1,2]
target = 0
```

Step 1 → mid = 3 → value 7
Left half sorted → target not in it → search right

Step 2 → mid = 5 → value 1
Right half sorted → target in it → search left

Step 3 → mid = 4 → found ✔

---

## ✅ Complexity Analysis

```text
Time  : O(log n)
Space : O(1)
```

Because we eliminate half of the array each step.

---

## ❌ Common Mistakes

| Mistake                            | Fix                                          |
| ---------------------------------- | -------------------------------------------- |
| Using `<` instead of `<=`          | Causes failure for small arrays like `[3,1]` |
| Not checking sorted half correctly | Always compare `nums[low]` & `nums[mid]`     |
| Using `(l+r)/2`                    | Use `l+(r-l)/2` to avoid overflow            |
| Forgetting edge cases              | Empty array, single element                  |

---

## ✅ Edge Cases

```text
[3,1], target=1 → 1
[1], target=0 → -1
[], target=5 → -1
```

---

## ✅ When This Problem Appears

* LeetCode 33
* Interviews (Amazon, Microsoft, etc.)
* System search logic problems

