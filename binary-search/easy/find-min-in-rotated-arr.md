
# Find Minimum in Rotated Sorted Array — Quick Revision

## Problem

Given a **sorted array that has been rotated**, find the **minimum element**.

Example:

```
Input:  [4,5,6,7,0,1,2]
Output: 0
```

Original sorted array:

```
[0,1,2,4,5,6,7]
```

After rotation:

```
[4,5,6,7,0,1,2]
```

Goal → **Find the smallest element in O(log n)**.

---

# Key Observation

In a rotated sorted array:

* One half is **sorted**
* One half is **unsorted**
* The **minimum always lies in the unsorted half**

Example:

```
[4,5,6,7,0,1,2]
```

```
Left half  → [4,5,6,7]
Right half → [0,1,2]
```

The **minimum is where the order breaks**.

---

# Binary Search Idea

Instead of comparing with `left`, compare **mid with right**.

```
nums[mid] vs nums[right]
```

---

## Case 1

```
nums[mid] > nums[right]
```

Example:

```
[4,5,6,7,0,1,2]
       ^
      mid
```

This means:

* The **minimum is in the right half**

Update:

```
left = mid + 1
```

---

## Case 2

```
nums[mid] <= nums[right]
```

Example:

```
[4,5,6,7,0,1,2]
          ^
         mid
```

This means:

* Minimum is **mid or to the left**

Update:

```
right = mid
```

---

# Loop Condition

```
while(left < right)
```

Why?

When:

```
left == right
```

that index **must be the minimum**.

---

# Final Code

```java
class Solution {
    public int findMin(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while(left < right){

            int mid = (left + right) / 2;

            if(nums[mid] > nums[right]){
                left = mid + 1;
            }
            else{
                right = mid;
            }
        }

        return nums[left];
    }
}
```

---

# Example Dry Run

Array:

```
[4,5,6,7,0,1,2]
```

Step 1

```
left=0 right=6
mid=3
nums[mid]=7
nums[right]=2
```

```
7 > 2
left = 4
```

---

Step 2

```
left=4 right=6
mid=5
nums[mid]=1
nums[right]=2
```

```
1 <= 2
right = 5
```

---

Step 3

```
left=4 right=5
mid=4
nums[mid]=0
nums[right]=1
```

```
0 <= 1
right = 4
```

Now:

```
left = right = 4
```

Return:

```
nums[4] = 0
```

---

# Complexity

Time Complexity

```
O(log n)
```

Space Complexity

```
O(1)
```

---

# Important Interview Rules

1️⃣ Use

```
while(left < right)
```

not `<=`

2️⃣ When shrinking right side

```
right = mid
```

not `mid - 1`

3️⃣ Always compare

```
nums[mid] vs nums[right]
```

---

# 1-Line Memory Trick

👉 **Minimum always lies in the unsorted half of the rotated array.**

Binary search simply **keeps discarding the sorted half**.
