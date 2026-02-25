
# ✅ Search Insert Position (Binary Search)

🔗 **LeetCode Problem:**
[https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)

---

## 🔹 Problem Samjho Simple Language Mein 😄

Given ek **sorted array** aur ek **target number**.

👉 Agar target mil gaya → uska index return karo
👉 Agar nahi mila → batao kaha insert hoga sorted order maintain karne ke liye

⚡ Runtime must be **O(log n)** → so Binary Search use karna padega.

---

## 🔹 Example Samjho

```id="r1p2z8"
nums = [1,3,5,6], target = 5 → Output = 2
```

```id="z0m8ql"
nums = [1,3,5,6], target = 2 → Output = 1
```

```id="5k3mta"
nums = [1,3,5,6], target = 7 → Output = 4
```

Basically target ko array mein **correct jagah** dhoondhni hai.

---

# ✅ Approach (Binary Search Logic 😎)

Array sorted hai → binary search best.

### Steps

1️⃣ Check if target smallest se bhi chota → index `0`
2️⃣ Check if target biggest se bada → index `n`

3️⃣ Binary search karo:

```id="c8l2qe"
nums[mid] == target → mil gaya → return mid

nums[mid] < target → target right side mein → left = mid+1

nums[mid] > target → target left side mein → right = mid-1
```

4️⃣ Loop khatam → `left` hi correct insert position hota hai.

---

# ✅ Code (Java)

```java id="7n9kpf"
class Solution {
    public int searchInsert(int[] nums, int target) {
        int n = nums.length;
        if(target > nums[n-1]){
            return n;
        }

        if(target < nums[0]){
            return 0;
        }

        int left = 0;
        int right = n-1;

        while(left <= right){
            int mid = (left + right)/2;
            if(nums[mid] == target){
                return mid;
            }
            else if(nums[mid] < target){
                left=mid+1;
            }
            else{
                right=mid-1;
            }
        }
        return left;
    }
}
```

---

# ✅ Edge Cases

```id="4s2pqm"
target smallest se chota → index 0
target biggest se bada → index n
target exist karta → exact index
```

---

# ✅ Time & Space Complexity

```id="3r2qzv"
Time Complexity  : O(log n)
Space Complexity : O(1)
```

Binary search har step mein array half karta hai.

---

# ✅ One-Line Memory Trick 🧠

```id="5r7pvn"
nums[mid] < target → right jao
nums[mid] > target → left jao
Loop end → left = insert position
```

