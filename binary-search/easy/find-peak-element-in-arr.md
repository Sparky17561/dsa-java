
# Find Peak Element — Binary Search

## Problem

Given an integer array `nums`, find a **peak element** and return its index.

A **peak element** is an element that is **strictly greater than its neighbors**.

Important rule:

```
nums[-1] = -∞
nums[n]  = -∞
```

So the first or last element **can also be a peak**.

---

## Example

```
Input:
nums = [1,2,3,1]

Output:
2
```

Explanation

```
3 > 2
3 > 1
```

So index `2` is a peak.

---

# Key Observation

If we compare:

```
nums[mid] vs nums[mid+1]
```

There are only **two possibilities**.

---

## Case 1 — Ascending slope

```
nums[mid] < nums[mid+1]
```

Example

```
1 2 3 4 5
      ^
     mid
```

The slope goes **upwards**, so a peak **must exist on the right side**.

Move search right:

```
left = mid + 1
```

---

## Case 2 — Descending slope

```
nums[mid] > nums[mid+1]
```

Example

```
5 4 3 2
 ^
mid
```

The slope goes **downwards**, so a peak **must exist on the left side or at mid**.

Move search left:

```
right = mid
```

We keep `mid` because **mid itself might be the peak**.

---

# Binary Search Algorithm

1. Initialize pointers

```
left = 0
right = n-1
```

2. Run binary search

```
while(left < right)
```

3. Compare

```
nums[mid] vs nums[mid+1]
```

4. Move search space accordingly.

---

# Java Implementation

```java
class Solution {

    // we go unidirectional .. the path is determined by mid and mid+1

    public int findPeakElement(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while(left < right){

            int mid = (left + right) / 2;

            if(nums[mid] < nums[mid+1]){
                left = mid + 1;
            }
            else{
                right = mid;
            }
        }

        return left;
    }
}
```

---

# Why Return `left` Instead of `mid`

`mid` is only a **temporary pointer** used to decide the direction.

Binary search keeps shrinking the range:

```
[left .... right]
```

When the loop stops:

```
left == right
```

The range contains **only one element**, which must be a **peak**.

So we return:

```
return left
```

(or `right`, both are same).

---

# Example Dry Run

Input

```
nums = [1,2,3,1]
```

Step 1

```
left = 0
right = 3
mid = 1
```

```
nums[mid] = 2
nums[mid+1] = 3
```

```
2 < 3
```

Move right side

```
left = mid + 1 = 2
```

---

Step 2

```
left = 2
right = 3
mid = 2
```

```
nums[mid] = 3
nums[mid+1] = 1
```

```
3 > 1
```

Move left side

```
right = mid = 2
```

---

Now

```
left = right = 2
```

Return

```
2
```

---

# Complexity

### Time Complexity

```
O(log n)
```

Binary search halves the search space.

### Space Complexity

```
O(1)
```

No extra space used.

---

# Important Insight

We are **not searching for the peak directly**.

Instead we follow the **slope direction**.

```
upward slope   → peak on right
downward slope → peak on left
```

Binary search keeps moving **toward a peak**.

---

# 10-Second Memory Trick

Just remember this rule:

```
nums[mid] < nums[mid+1] → go right
nums[mid] > nums[mid+1] → go left
```

Loop until

```
left == right
```

Return that index.

---

# Edge Cases

Works for all cases:

```
[5,10,20,15]
[10,20,15,2,23,90,67]
[1,3,2,5,4,7,6]
[1,2,3,4,5]
[5,4,3,2,1]
[1]
```

The algorithm finds **any valid peak**.

