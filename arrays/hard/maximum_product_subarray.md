# 📘 Maximum Product Subarray 

---

## 🔎 Problem Understanding

We need to find the **contiguous subarray** that has the **maximum product** and return that product.

Unlike the Maximum Sum Subarray (Kadane’s), this problem is tricky because of **negative numbers**.

---

# 🧠 Intuition

Multiplication behaves differently from addition:

* Negative × Positive = Negative
* Negative × Negative = Positive

This means:

👉 A very small (most negative) product can suddenly become the largest positive product when multiplied by another negative number.

So at every index, we must track:

1. **Maximum product ending at that index**
2. **Minimum product ending at that index**

Why track minimum?

Because today's minimum (negative) might become tomorrow’s maximum when multiplied by another negative.

---

# ⚙️ Core Idea

At each index `i`:

* If the number is negative → swap `max` and `min`
* Update:

  ```
  max = max(nums[i], nums[i] * max)
  min = min(nums[i], nums[i] * min)
  ```
* Update global result

---

# 🧮 Algorithm

### Initialization

```
max = nums[0]
min = nums[0]
res = nums[0]
```

### Traverse from index 1

For every `nums[i]`:

1. If negative → swap max & min
2. Update max
3. Update min
4. Update result

---

# 🧪 Dry Run Example

### Input:

```
[-2, 3, -4]
```

---

### Step 0 (Initialize)

```
max = -2
min = -2
res = -2
```

---

### i = 1 → 3

Number is positive → no swap

```
max = max(3, 3 * -2) = 3
min = min(3, 3 * -2) = -6
res = max(-2, 3) = 3
```

State:

```
max = 3
min = -6
res = 3
```

---

### i = 2 → -4

Number is negative → swap

Before swap:

```
max = 3
min = -6
```

After swap:

```
max = -6
min = 3
```

Now update:

```
max = max(-4, -6 * -4) = 24
min = min(-4, 3 * -4) = -12
res = max(3, 24) = 24
```

---

### Final Answer:

```
24
```

---

# 📌 Why Swap Works

If current number is negative:

* max × negative → becomes negative
* min × negative → becomes positive

So roles reverse.

That’s why swapping is necessary.

---

# 🧾 Final Code

```java
class Solution {
    public int maxProduct(int[] nums) {
        int res = nums[0];
        int min = nums[0];
        int max = nums[0];

        for(int i = 1; i < nums.length; i++) {

            if(nums[i] < 0){
                int temp = max;
                max = min;
                min = temp;
            }

            max = Math.max(nums[i], max * nums[i]);
            min = Math.min(nums[i], min * nums[i]);

            res = Math.max(res, max);
        }
        return res;
    }
}
```

---

# ⏱ Time Complexity

We traverse the array once.

```
Time Complexity = O(n)
```

---

# 🧠 Space Complexity

We use only three variables (`max`, `min`, `res`).

```
Space Complexity = O(1)
```

---

# 🎯 Interview One-Liner

> Track both maximum and minimum product at every index because a negative number can flip the smallest product into the largest one.

