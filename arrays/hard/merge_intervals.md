# Merge Intervals

## 🧠 Problem

Given an array of intervals where `intervals[i] = [start, end]`,
merge all overlapping intervals and return a new array of non-overlapping intervals.

---

## 🔎 Key Idea

1. **Sort intervals by starting time**
2. Compare current interval with the previous merged interval
3. If overlapping → merge
4. If not overlapping → add previous to result and move ahead

---

## ⚙️ Why Sorting is Important?

Without sorting:

```
[[1,4],[0,2],[3,5]]
```

You may incorrectly merge because order is random.

After sorting:

```
[[0,2],[1,4],[3,5]]
```

Now merging becomes logical from left to right.

---

## 🧩 Core Logic (Your Fixed Version Concept)

* Store first interval in `temp`
* Iterate from `i = 1`
* If overlapping:

  * Update `temp[0]` → min start
  * Update `temp[1]` → max end
* Else:

  * Add `temp` to result
  * Move `temp` to current interval
* Finally add last `temp`

---

## ✅ Final Code

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        int n = intervals.length;
        int i = 1;
        List<int[]> res = new ArrayList<>();

        if (n <= 1) return intervals;

        // Step 1: Sort intervals by start time
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        int[] temp = intervals[0];

        while (i < n) {
            if (temp[1] >= intervals[i][0]) {
                // Merge
                temp[0] = Math.min(temp[0], intervals[i][0]);
                temp[1] = Math.max(temp[1], intervals[i][1]);
            } else {
                // No overlap
                res.add(temp);
                temp = intervals[i];
            }
            i++;
        }

        res.add(temp);

        return res.toArray(new int[res.size()][]);
    }
}
```

---


## 🕒 Time Complexity

* Sorting → `O(n log n)`
* Single pass merge → `O(n)`
* Overall → `O(n log n)`

---

## 📌 Edge Cases

* Only 1 interval → return as it is
* Fully overlapping intervals
* Fully non-overlapping intervals
* One interval covering all others

---

## 🎯 Final Concept in One Line (Quick Revision)

> Sort → Compare with last merged interval → Merge if overlapping → Else push to result.

