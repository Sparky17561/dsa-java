
# Search in Rotated Sorted Array II — Binary Search

## Problem

Given a **rotated sorted array** `nums` that **may contain duplicates**, determine if a **target value exists** in the array.

Return:

```
true  → if target exists
false → otherwise
```

---

## Example

```text
Input:
nums = [2,5,6,0,0,1,2]
target = 0

Output:
true
```

```text
Input:
nums = [2,5,6,0,0,1,2]
target = 3

Output:
false
```

---

# Key Idea

A rotated array always has **one sorted half**.

We can use **Binary Search** to determine:

```
1. Which half is sorted
2. Whether the target lies inside that half
```

However, because **duplicates exist**, sometimes we **cannot determine which side is sorted**.

In that case we **shrink the search range**.

---

# Binary Search Strategy

At each step compute:

```
mid = (left + right) / 2
```

---

## Case 1 — Target Found

```
nums[mid] == target
```

Return:

```
true
```

---

## Case 2 — Duplicates Prevent Decision

Example

```
[1,1,1,1,3,1]
 L M       R
```

Here

```
nums[left] == nums[mid] == nums[right]
```

We cannot determine the sorted side.

Shrink search space:

```
left++
right--
```

---

## Case 3 — Left Half Sorted

Condition:

```
nums[left] <= nums[mid]
```

Check if target lies inside this range:

```
nums[left] <= target < nums[mid]
```

If true:

```
right = mid - 1
```

Otherwise:

```
left = mid + 1
```

---

## Case 4 — Right Half Sorted

If left half is not sorted, the **right half must be sorted**.

Check:

```
nums[mid] < target <= nums[right]
```

If true:

```
left = mid + 1
```

Otherwise:

```
right = mid - 1
```

---

# Java Implementation

```java
class Solution {
    public boolean search(int[] nums, int target) {

        int left = 0;
        int right = nums.length - 1;

        while(left <= right){

            int mid = (left + right) / 2;

            if(nums[mid] == target){
                return true;
            }

            // duplicates case
            if(nums[left] == nums[mid] && nums[mid] == nums[right]){
                left++;
                right--;
            }

            // left side sorted
            else if(nums[left] <= nums[mid]){

                if(nums[left] <= target && target < nums[mid]){
                    right = mid - 1;
                }
                else{
                    left = mid + 1;
                }
            }

            // right side sorted
            else{

                if(nums[mid] < target && target <= nums[right]){
                    left = mid + 1;
                }
                else{
                    right = mid - 1;
                }
            }
        }

        return false;
    }
}
```

---

# Example Dry Run

```
nums = [2,5,6,0,0,1,2]
target = 0
```

Step 1

```
left = 0
right = 6
mid = 3
```

```
nums[mid] = 0
```

Target found → return **true**.

---

# Complexity

### Best / Average Case

```
O(log n)
```

Binary search halves the search space.

### Worst Case (many duplicates)

```
O(n)
```

Example

```
[1,1,1,1,1,1,1,2,1]
```

Duplicates force shrinking one step at a time.

---

# Quick Interview Memory Trick

Follow this order:

```
1. nums[mid] == target → return true
2. nums[left] == nums[mid] == nums[right] → shrink
3. left half sorted → check target range
4. right half sorted → check target range
```

---

# Edge Cases

Works for:

```
[1]
[1,1,1,1]
[1,3,1,1,1]
[2,2,2,3,2,2]
```

---

# One-Line Intuition

Binary search always works because:

```
At least one half of the rotated array is sorted.
```

We just **identify the sorted half and decide which direction to search**.

