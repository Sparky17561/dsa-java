
# 📘 README 1 — Count Occurrences in Sorted Array

## ✅ Problem

Given a **sorted array**, count how many times `target` appears.

Example:

```
arr = [1,2,2,2,3]
target = 2
answer = 3
```

---

## ✅ Idea

Use **Binary Search twice**

1️⃣ Find **first occurrence**
2️⃣ Find **last occurrence**
3️⃣ Count = `last - first + 1`

Why?
Because array is sorted → binary search works.

---

## ✅ Steps

```
1. first = findFirst(arr,target)
2. if first == -1 → return 0
3. last = findLast(arr,target)
4. return last-first+1
```

---

## ✅ Code

```java
class Solution {
    public int countOccurrences(int[] arr, int target) {

        int first = findFirst(arr, target);
        if(first == -1) return 0;

        int last = findLast(arr, target);

        return last - first + 1;
    }

    private int findFirst(int[] arr, int target){
        int left = 0, right = arr.length - 1;
        int ans = -1;

        while(left <= right){
            int mid = left + (right-left)/2;

            if(arr[mid] == target){
                ans = mid;
                right = mid - 1;
            }
            else if(arr[mid] < target){
                left = mid + 1;
            }
            else{
                right = mid - 1;
            }
        }
        return ans;
    }

    private int findLast(int[] arr, int target){
        int left = 0, right = arr.length - 1;
        int ans = -1;

        while(left <= right){
            int mid = left + (right-left)/2;

            if(arr[mid] == target){
                ans = mid;
                left = mid + 1;
            }
            else if(arr[mid] < target){
                left = mid + 1;
            }
            else{
                right = mid - 1;
            }
        }
        return ans;
    }
}
```

---

## ✅ Complexity

```
Time  : O(log n)
Space : O(1)
```

---

## ❌ Common Mistakes

| Mistake                | Fix                        |
| ---------------------- | -------------------------- |
| Using `(l+r)/2`        | Use `l+(r-l)/2`            |
| Using `break`          | Always move left/right     |
| Not resetting pointers | Reset before second search |
| Wrong variable name    | arr vs nums                |

---

## ✅ Interview Tip

Say:

👉 “Because array sorted, I use binary search to find first and last occurrence.”

---

---

# 📘 README 2 — LeetCode Search Range (First & Last Position)

## ✅ Problem

LeetCode: **Find First and Last Position of Element**

Return `[first,last]`.

If not found → `[-1,-1]`.

Example:

```
nums = [5,7,7,8,8,10]
target = 8
output = [3,4]
```

---

## ✅ Idea

Same as previous problem.

Binary search twice.

But return array instead of count.

---

## ✅ Steps

```
1. first = findFirst()
2. if first == -1 → return [-1,-1]
3. last = findLast()
4. return [first,last]
```

---

## ✅ Code (Your Correct Solution)

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {

        int left = 0, right = nums.length - 1;
        int first = -1, last = -1;

        while(left <= right){
            int mid = left + (right-left)/2;

            if(nums[mid] == target){
                first = mid;
                right = mid - 1;
            }
            else if(nums[mid] < target){
                left = mid + 1;
            }
            else{
                right = mid - 1;
            }
        }

        left = 0;
        right = nums.length - 1;

        while(left <= right){
            int mid = left + (right-left)/2;

            if(nums[mid] == target){
                last = mid;
                left = mid + 1;
            }
            else if(nums[mid] < target){
                left = mid + 1;
            }
            else{
                right = mid - 1;
            }
        }

        return new int[]{first,last};
    }
}
```

---

## ✅ Edge Cases

| Case               | Output  |
| ------------------ | ------- |
| Empty array        | [-1,-1] |
| Target not present | [-1,-1] |
| Single element     | [0,0]   |

---

## ✅ Complexity

```
Time  : O(log n)
Space : O(1)
```

---

## ✅ Why Two Binary Searches?

Because duplicates may exist.

One search can’t guarantee first/last.

---

## ✅ Alternate Trick

Use:

```
lowerBound = first index >= target
upperBound = first index > target
count = upper-lower
```

