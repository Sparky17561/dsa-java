# Single Element in a Sorted Array — Binary Search

## Problem

Given a **sorted array** where:

* Every element appears **exactly twice**
* Only **one element appears once**

Find the **single non-duplicate element**.

### Example

```
Input:
[1,1,2,2,3,4,4,5,5]

Output:
3
```

### Constraints

* Time complexity required: **O(log n)**
* Space complexity: **O(1)**

This means we must use **Binary Search**.

---

# Key Observation

Since the array is **sorted**, duplicates always appear **next to each other**.

### Before the single element

Pairs start at **even indices**.

```
Index: 0 1 2 3 4 5
Array: 1 1 2 2 3 3
Pairs: (0,1) (2,3) (4,5)
```

Pattern:

```
nums[even] == nums[even+1]
```

---

### After the single element

The pattern **shifts**.

Example:

```
[1,1,2,2,3,4,4,5,5]
           ^
         single
```

Now pairs start at **odd indices**.

```
Index: 5 6 7 8
Pairs: (5,6) (7,8)
```

Pattern breaks.

---

# Binary Search Strategy

We use binary search to detect **where the pattern breaks**.

Steps:

1. Calculate `mid`
2. Force `mid` to be **even**
3. Compare:

```
nums[mid] with nums[mid+1]
```

---

### Case 1

```
nums[mid] == nums[mid+1]
```

Pair is correct → single element is **right side**

```
left = mid + 2
```

---

### Case 2

```
nums[mid] != nums[mid+1]
```

Pattern broken → single element is **left side**

```
right = mid
```

---

# Algorithm

1. Initialize `left = 0`, `right = n-1`
2. Run binary search while `left < right`
3. Adjust `mid` to even index
4. Compare pair elements
5. Narrow the search space

---

# Java Implementation

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while(left < right){

            int mid = (left + right) / 2;

            if(mid % 2 == 1){
                mid--;        // ensure mid is even
            }

            if(nums[mid] == nums[mid+1]){
                left = mid + 2;
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

# Dry Run Example

Array:

```
[1,1,2,2,3,4,4,5,5]
```

### Step 1

```
left = 0
right = 8
mid = 4
```

Compare:

```
nums[4] = 3
nums[5] = 4
```

Not equal → single is **left side**

```
right = 4
```

---

### Step 2

```
left = 0
right = 4
mid = 2
```

Compare:

```
nums[2] = 2
nums[3] = 2
```

Equal → single is **right side**

```
left = 4
```

---

Now:

```
left = right = 4
```

Return:

```
nums[4] = 3
```

---

# Complexity

### Time Complexity

```
O(log n)
```

Binary search halves the search space each step.

### Space Complexity

```
O(1)
```

No extra memory used.

---

# Quick Interview Memory Trick

Remember this rule:

```
Before single → pairs start at even index
After single  → pairs start at odd index
```

So we **force mid to even** and check:

```
nums[mid] == nums[mid+1]
```

If true → move **right**
If false → move **left**

