# 📘 Length of Longest Subarray with Zero Sum – README

---

## 🔎 Problem Statement

Given an array containing **both positive and negative integers**, find the **length of the longest contiguous subarray** whose sum is equal to **0**.

---

## 🧠 Intuition

The key idea is based on **prefix sum**.

### What is Prefix Sum?

At index `i`:

```
prefixSum = arr[0] + arr[1] + ... + arr[i]
```

---

### 🔥 Important Observation

If at two different indices `i` and `j`:

```
prefixSum[i] == prefixSum[j]
```

Then the subarray between `(i+1)` and `j` must have sum = 0.

Why?

Because:

```
sum(0 → j) - sum(0 → i) = 0
```

So if the same prefix sum appears again → the elements between those indices cancel out.

---

## ⚙️ Core Idea

We:

1. Keep a running prefix sum.
2. Store first occurrence of each prefix sum in a HashMap.
3. If the same sum appears again:

   * We calculate subarray length.
4. Keep track of maximum length.

---

## 📌 Algorithm Steps

1. Initialize:

   * `sum = 0`
   * `maxLen = 0`
   * `HashMap<sum, index>`

2. Traverse array:

   * Add element to sum.
   * If sum == 0 → subarray from start has zero sum.
   * If sum already exists in map → zero-sum subarray found.
   * Otherwise store sum and index in map.

3. Return `maxLen`.

---

# 🧪 Dry Run Example

### Example:

```
arr = {9, -3, 3, -1, 6, -5}
```

---

### Step-by-step

| Index | Value | Running Sum | Map                   | maxLen |
| ----- | ----- | ----------- | --------------------- | ------ |
| 0     | 9     | 9           | {9:0}                 | 0      |
| 1     | -3    | 6           | {9:0, 6:1}            | 0      |
| 2     | 3     | 9           | 9 seen before at 0    | 2      |
| 3     | -1    | 8           | {9:0, 6:1, 8:3}       | 2      |
| 4     | 6     | 14          | {9:0, 6:1, 8:3, 14:4} | 2      |
| 5     | -5    | 9           | 9 seen before at 0    | 5      |

---

### How length = 5?

At index 5:

```
sum = 9
```

We saw 9 earlier at index 0.

So subarray:

```
index 1 → 5
```

Length:

```
5 - 0 = 5
```

---

## 🧾 Code with Detailed Comments

```java
import java.util.HashMap;

class Solution {
    public int maxLen(int[] arr) {

        // Stores maximum length of zero sum subarray
        int maxLen = 0;

        // Stores prefix sum while traversing
        int sum = 0;

        // Map to store prefixSum as key and its first occurrence index as value
        HashMap<Integer, Integer> map = new HashMap<>();

        for(int i = 0; i < arr.length; i++) {

            // Add current element to running sum
            sum += arr[i];

            // Case 1: If prefix sum becomes 0,
            // then subarray from 0 to i has zero sum
            if(sum == 0) {
                maxLen = i + 1;
            }

            else {

                // Case 2: If this sum was seen before
                if(map.containsKey(sum)) {

                    // Length of subarray between previous index+1 and current index
                    int length = i - map.get(sum);

                    maxLen = Math.max(maxLen, length);
                }

                // Case 3: First time seeing this sum
                // Store only first occurrence
                else {
                    map.put(sum, i);
                }
            }
        }

        return maxLen;
    }
}
```

---

## ⏱ Time Complexity

We traverse array once and HashMap operations are O(1).

```
Time Complexity = O(n)
```

---

## 🧠 Space Complexity

In worst case, all prefix sums are different.

```
Space Complexity = O(n)
```

---

## 🎯 Why We Store Only First Occurrence?

Because we want the **longest** subarray.

If we overwrite index in map, we might lose earlier occurrence → shorter length.

---

## 🏁 Final Summary

* Use prefix sum
* If same sum appears again → zero-sum subarray exists
* Use HashMap to store first occurrence
* Update maximum length accordingly

