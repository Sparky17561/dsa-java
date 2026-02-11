# 4Sum

## 🧠 Problem

Given an integer array `nums` and an integer `target`, return **all unique quadruplets**
`[nums[a], nums[b], nums[c], nums[d]]` such that:

```
a, b, c, d are distinct indices
nums[a] + nums[b] + nums[c] + nums[d] == target
```

Return the answer without duplicate quadruplets.

---

## 💡 Intuition

This is an extension of:

* 2Sum → Two pointers
* 3Sum → Fix 1 number + Two pointers
* 4Sum → Fix 2 numbers + Two pointers

### Strategy:

1. Sort the array.
2. Fix first number (`i`).
3. Fix second number (`j`).
4. Use two pointers (`left`, `right`) to find remaining two numbers.
5. Skip duplicates at every level.

---

## ⚙️ Why Sorting?

Sorting helps:

* Use two-pointer technique.
* Easily skip duplicates.
* Avoid repeated quadruplets.

Example:

```
Input: [1,0,-1,0,-2,2]
After sort: [-2,-1,0,0,1,2]
```

---

## 🚀 Algorithm

1. Sort the array.
2. Loop `i` from `0` to `n-4`

   * Skip duplicates for `i`
3. Loop `j` from `i+1` to `n-3`

   * Skip duplicates for `j`
4. Set:

   ```
   left = j + 1
   right = n - 1
   ```
5. While `left < right`:

   * Compute sum using `long` (to prevent overflow)
   * If sum == target → store result
   * Move pointers accordingly
   * Skip duplicates for `left` and `right`

---

## ✅ Final Code

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> res = new ArrayList<>();
        int n = nums.length;
        if(n < 4) return res;

        Arrays.sort(nums);

        for(int i = 0; i < n - 3; i++) {

            if(i > 0 && nums[i] == nums[i - 1]) continue;

            for(int j = i + 1; j < n - 2; j++) {

                if(j > i + 1 && nums[j] == nums[j - 1]) continue;

                int left = j + 1;
                int right = n - 1;

                while(left < right) {

                    long sum = (long) nums[i] 
                             + nums[j] 
                             + nums[left] 
                             + nums[right];

                    if(sum == target) {

                        res.add(Arrays.asList(
                                nums[i], nums[j], 
                                nums[left], nums[right]
                        ));

                        left++;
                        right--;

                        while(left < right && nums[left] == nums[left - 1])
                            left++;

                        while(left < right && nums[right] == nums[right + 1])
                            right--;
                    }
                    else if(sum > target) {
                        right--;
                    }
                    else {
                        left++;
                    }
                }
            }
        }
        return res;
    }
}
```

---

## 🧪 Dry Run Example

### Input:

```
nums = [1,0,-1,0,-2,2]
target = 0
```

After sorting:

```
[-2,-1,0,0,1,2]
```

Valid quadruplets:

```
[-2,-1,1,2]
[-2,0,0,2]
[-1,0,0,1]
```

---

## ⚠️ Important Edge Case – Overflow

If numbers are large (like `10^9`):

```
1000000000 * 4 = 4000000000
```

This exceeds `int` limit.

So we use:

```java
long sum
```

To prevent overflow errors.

---

## 🕒 Time Complexity

* Sorting → `O(n log n)`
* Nested loops → `O(n³)`
* Overall → **O(n³)**

---

## 💾 Space Complexity

* Extra space for result → depends on output
* No extra data structures used

**Auxiliary Space → O(1)** (excluding result storage)

---

## 🎯 Key Interview Points

* Always sort first.
* Always skip duplicates at all 3 levels.
* Always use `long` for sum in 4Sum.
* Two-pointer technique reduces one loop.

---

## 🧠 Pattern Recognition

```
2Sum → O(n)
3Sum → O(n²)
4Sum → O(n³)
kSum → O(n^(k-1))
```
