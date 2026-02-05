
# Longest Consecutive Sequence (Java)

### 📖 Problem Overview

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

* **Example:** Input `[100, 4, 200, 1, 3, 2]`  Output `4` (Sequence: `1, 2, 3, 4`)

---

## Approach 1: The Sorting Strategy

**Logic:** If we sort the array, consecutive numbers will sit next to each other. We iterate through the sorted array and count the length of current sequences.

### 💻 Code

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) return 0;
        
        Arrays.sort(nums); // The bottleneck: O(N log N)
        
        int longest = 1;
        int currentStreak = 1;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i-1]) { // Ignore duplicates
                if (nums[i] == nums[i-1] + 1) {
                    currentStreak++;
                } else {
                    longest = Math.max(longest, currentStreak);
                    currentStreak = 1;
                }
            }
        }
        return Math.max(longest, currentStreak);
    }
}

```

### 📊 Complexity

* **Time:**  because of sorting.
* **Space:**  (or  depending on the sorting algorithm used internally).
* **Pros:** Easy to understand, low memory usage.
* **Cons:** Too slow for very large datasets required by strict  constraints.

---

## Approach 2: The HashSet Strategy (Optimal)

**Logic:** To achieve linear time , we use a `HashSet` for instant lookups.

1. Add all numbers to a Set.
2. Iterate through the Set.
3. **Smart Optimization:** Only attempt to count a sequence if the current number is the **START** of a sequence (i.e., `num - 1` does not exist in the set). This ensures we visit each number at most twice.

### 💻 Code

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) return 0;

        HashSet<Integer> set = new HashSet<>();
        for (int n : nums) { 
            set.add(n); 
        }

        int max = 0;

        for (int num : set) {
            // Check if 'num' is the start of a sequence
            if (!set.contains(num - 1)) {
                int currentNum = num;
                int currentStreak = 1;

                // Expand the sequence
                while (set.contains(currentNum + 1)) {
                    currentNum++;
                    currentStreak++;
                }

                max = Math.max(max, currentStreak);
            }
        }
        return max;
    }
}

```

### 📊 Complexity

* **Time:** . We iterate the array once to build the set, and the inner `while` loop runs only when a sequence starts. Total operations are linear.
* **Space:**  to store elements in the HashSet.
* **Pros:** Fastest possible time complexity.
* **Cons:** Uses extra memory.

---

## ⚔️ Comparison Cheat Sheet

| Feature | Sorting Approach | HashSet Approach |
| --- | --- | --- |
| **Speed** | Slower () | **Fastest ()** |
| **Memory** | **Low ()** | High () |
| **Handling Duplicates** | Needs explicit `if` check | Automatically handled by Set |
| **Interview Verdict** | "Good start, but optimize it." | **"Perfect."** |

### 🚀 Key Logic to Remember

For the optimal solution, always ask: **"Is `num - 1` in the set?"**

* **Yes?**  Skip it (it's not the start).
* **No?**  Start counting!