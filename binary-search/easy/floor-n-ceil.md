
# ✅ Floor and Ceil in Sorted Array

## 🔹 Problem

Given a **sorted array `nums`** and an integer `x`:

* **Floor** → Largest element ≤ `x`
* **Ceil** → Smallest element ≥ `x`
* If no such value exists → return `-1`

---

## 🔹 Examples

```text
nums = [3, 4, 4, 7, 8, 10], x = 5
Output → 4 7
```

```text
nums = [3, 4, 4, 7, 8, 10], x = 8
Output → 8 8
```

---

# ✅ Approach (Binary Search)

Since the array is **sorted**, we use **binary search**.

### Idea

1. Keep two variables → `floor` and `ceil`
2. Start with `left = 0`, `right = n-1`
3. Find `mid`
4. Compare `nums[mid]` with `x`

### Cases

```text
nums[mid] == x
    floor = ceil = nums[mid]

nums[mid] < x
    update floor
    move right

nums[mid] > x
    update ceil
    move left
```

Continue until search space ends.

---

# ✅ Code (Java)

```java
class Solution {
    public int[] getFloorAndCeil(int[] nums, int x) {
       int n = nums.length;
       int floor=-1;
       int ceil=-1;
       int left = 0, right = n-1;
       int [] arr = new int[2];
       while(left<=right){
            int mid = (left+right)/2;
            if(nums[mid] == x){
                floor = ceil = nums[mid];
                break;

            }
            else if(nums[mid] < x){
                floor = nums[left];
                left = mid + 1;
            }
            else{
                ceil = nums[right];
                right = mid - 1;
            }
       }
        arr[0] = floor;
        arr[1] = ceil;
        return arr;
    }
}
```

---

# ✅ Edge Cases

```text
x smaller than all → floor = -1
x larger than all → ceil = -1
x present in array → floor = ceil = x
```

---

# ✅ Time & Space Complexity

```text
Time Complexity  : O(log n)
Space Complexity : O(1)
```

Binary search reduces search space by half each step.

---

# ✅ Quick Memory Trick

```text
nums[mid] < x → update floor → go right
nums[mid] > x → update ceil  → go left
```

