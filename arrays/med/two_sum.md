Perfect — here’s a **complete, interview-ready README** you can paste directly into GitHub / notes, **plus both implementations** (Sorting + Two Pointers **and** HashMap), with **clear comparison**.

Reading time: **~1–2 minutes**, exactly what you asked for.

---

# 📘 Two Sum — Java Implementations & Trade-offs

## 🧠 Problem Statement

Given an integer array `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You may assume that **exactly one solution exists**, and you **may not use the same element twice**.

---

## 🚀 Approaches Covered

This repository includes **two valid approaches**:

1. **Sorting + Two Pointers**
2. **HashMap (One Pass)**

Both are interview-acceptable, but each has different **strengths and trade-offs**.

---

## 🔹 Approach 1: Sorting + Two Pointers

### 💡 Idea

1. Store each element along with its **original index**.
2. Sort the array based on values.
3. Use two pointers (`left`, `right`) to find the target sum.
4. Return the original indices when the sum matches.

This approach is useful for learning **reusable patterns** like:

* Two pointers
* Sorting custom objects
* Problems like 3Sum, Closest Sum, Interval problems

---

### ✅ Code (Sorting + Two Pointers)

```java
class Solution {

    // Pair class to store value and original index
    class Pair implements Comparable<Pair> {
        int val;
        int idx;

        Pair(int val, int idx) {
            this.val = val;
            this.idx = idx;
        }

        // Sort based on value
        public int compareTo(Pair o) {
            return this.val - o.val;
        }
    }

    public int[] twoSum(int[] nums, int target) {

        // Step 1: Create array of Pair objects
        Pair[] pairs = new Pair[nums.length];
        for (int i = 0; i < nums.length; i++) {
            pairs[i] = new Pair(nums[i], i);
        }

        // Step 2: Sort the pairs
        Arrays.sort(pairs);

        int left = 0;
        int right = pairs.length - 1;

        int[] res = new int[2];

        // Step 3: Two-pointer traversal
        while (left < right) {
            int sum = pairs[left].val + pairs[right].val;

            if (sum < target) {
                left++;
            } 
            else if (sum > target) {
                right--;
            } 
            else {
                // Target found
                res[0] = pairs[left].idx;
                res[1] = pairs[right].idx;
                break;
            }
        }

        return res;
    }
}
```

---

### ⏱ Complexity

* **Time:** `O(n log n)` (sorting)
* **Space:** `O(n)` (pair array)

---

### 📌 When this approach is useful

* Array is already sorted
* Need closest pair / range-based answers
* Want deterministic traversal
* Extends naturally to 3Sum / 4Sum

---

## 🔹 Approach 2: HashMap (Optimal for Two Sum)

### 💡 Idea

1. Traverse the array once.
2. For each element, check if `(target - current)` exists in the map.
3. If yes → solution found.
4. Else → store the current value and index.

This is the **most optimal** approach for classic Two Sum.

---

### ✅ Code (HashMap – One Pass)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int needed = target - nums[i];

            // If complement exists, return indices
            if (map.containsKey(needed)) {
                return new int[]{map.get(needed), i};
            }

            // Store current value with its index
            map.put(nums[i], i);
        }

        return new int[]{-1, -1}; // will never reach here as per problem statement
    }
}
```

---

### ⏱ Complexity

* **Time:** `O(n)`
* **Space:** `O(n)`

---

## ⚖️ HashMap vs Sorting — Comparison

| Feature                   | HashMap   | Sorting + Two Pointers |
| ------------------------- | --------- | ---------------------- |
| Time Complexity           | `O(n)` ✅  | `O(n log n)`           |
| Space Complexity          | `O(n)`    | `O(n)`                 |
| Best for Two Sum          | ✅ YES     | ❌ Slower               |
| Pattern Reusability       | ❌ Limited | ✅ High                 |
| Extends to 3Sum / Closest | ❌ Hard    | ✅ Easy                 |
| Deterministic traversal   | ❌         | ✅                      |

---

## 🗣️ Interview Answer (Use This)

> “HashMap gives an optimal O(n) solution for Two Sum, but I also implemented a sorting + two pointer approach because it generalizes well to problems like 3Sum and closest pair. It provides deterministic traversal and is useful when the array is already sorted.”

That answer shows **maturity**, not just optimization obsession.

---

## 🏁 Final Verdict

* ✔ **HashMap** → Best for classic Two Sum
* ✔ **Sorting + Two Pointers** → Best for pattern learning & extensions
* ✔ Knowing **both** = interview-ready


