
# Rearrange Array Elements by Sign (Java Solution)

### 📖 Problem Overview

You are given an array of integers containing an equal number of positive and negative numbers. You need to rearrange the array so that every consecutive pair of integers has opposite signs, starting with a positive number.

**Order must be preserved:** If `3` came before `5` in the original array, `3` must come before `5` in the final array.

### 💡 The Core Logic (The "Two Buckets" Strategy)

This solution uses a straightforward **divide and conquer** approach.

1. **Separate:** Imagine you have two buckets. You walk through the array and toss all positive numbers into the "Positive Bucket" and all negative numbers into the "Negative Bucket."
2. **Merge:** You empty the buckets back into the original array, alternating between taking one from the Positive bucket and one from the Negative bucket.

### ⚡ Step-by-Step Execution

1. **Initialization:** Create two `ArrayLists` (`pos` and `neg`) to act as our temporary buckets.
2. **First Pass (Segregation):** Loop through the input array `nums`.
* If the number is , add it to the `pos` list.
* If the number is , add it to the `neg` list.


3. **Second Pass (Reconstruction):** Loop through the original array length again.
* **Even Index (0, 2, 4...):** We need a positive number.
* **Odd Index (1, 3, 5...):** We need a negative number.



### 🧮 The Math Trick: `i / 2`

You might wonder how we get the correct index from the `pos` and `neg` lists using the main loop iterator `i`.

We use **Integer Division** (`i / 2`):

| Main Index (`i`) | Is it Even/Odd? | Math: `i / 2` | Result Source |
| --- | --- | --- | --- |
| **0** | Even |  | `pos.get(0)` |
| **1** | Odd |  | `neg.get(0)` |
| **2** | Even |  | `pos.get(1)` |
| **3** | Odd |  | `neg.get(1)` |

*This clever trick allows us to grab the 0th element for both the first positive and first negative slot, then the 1st element for the next pair, and so on.*

### 🔑 Key Knowledge & Concepts used

* **ArrayList vs Array:** You used `ArrayList` for the buckets because we didn't know initially how many positives or negatives there were (though the problem guarantees they are equal, using Lists is safer if they weren't).
* **Modulo Operator (`%`):** Used `i % 2 == 0` to identify even indices (places for positive numbers).
* **Integer Division:** Understanding that `1 / 2` in Java equals `0` (it drops the decimal) is crucial for this logic to work.

### 📊 Complexity Analysis

| Metric | Complexity | Explanation |
| --- | --- | --- |
| **Time** | **** | We iterate through the array twice (, which simplifies to ). |
| **Space** | **** | We create two extra lists that, combined, hold exactly  elements. |

Here is the addition to your README. You can append this section after the previous solution.

---

# ⚡ Optimized Solution: Two Pointers (Single Pass)

### 📖 Why optimize?

The previous solution works, but it iterates through the data **twice** (once to split, once to merge) and uses `ArrayLists` which are slower than raw arrays. This approach does it all in **one loop**.

### 💻 The Code

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int[] result = new int[n]; // Pre-allocate exact size
        
        // Pointers indicate the next available slot
        int posIndex = 0; // Starts at even index (0, 2, 4...)
        int negIndex = 1; // Starts at odd index (1, 3, 5...)

        for(int i = 0; i < n; i++) {
            if(nums[i] > 0) {
                result[posIndex] = nums[i];
                posIndex += 2; // Jump to next even slot
            } 
            else {
                result[negIndex] = nums[i];
                negIndex += 2; // Jump to next odd slot
            }
        }
        
        return result;
    }
}

```

### 💡 The Core Logic (The "Card Dealer" Strategy)

Imagine you are dealing cards into two piles on a table, but the spots on the table are fixed.

* **Positives** are strictly allowed only on spots 0, 2, 4, 6...
* **Negatives** are strictly allowed only on spots 1, 3, 5, 7...

Instead of separating the deck first, you pick up a card (iterate through `nums`), look at it, and immediately place it in its correct "next available spot," then move that spot's marker forward.

### ⚡ Step-by-Step Execution

Input: `[3, 1, -2, -5, 2, -4]`

1. **Setup:** `result` is empty. `posIndex` points to **0**. `negIndex` points to **1**.
2. **Scan `3` (+):** Place at `result[0]`. Move `posIndex` to **2**.
3. **Scan `1` (+):** Place at `result[2]`. Move `posIndex` to **4**.
4. **Scan `-2` (-):** Place at `result[1]`. Move `negIndex` to **3**.
5. **Scan `-5` (-):** Place at `result[3]`. Move `negIndex` to **5**.
*(...and so on)*

### 📊 Brute Force vs. Optimized Comparison

| Feature | Brute Force (ArrayList) | Optimized (Two Pointers) | Winner |
| --- | --- | --- | --- |
| **Passes** | 2 Passes | 1 Pass | **Optimized** |
| **Data Structure** | `ArrayList<Integer>` (High overhead) | `int[]` (Low overhead) | **Optimized** |
| **Resizing** | Lists resize dynamically as they grow | Array size is fixed initially | **Optimized** |
| **Time Complexity** |  (Slower constants) |  (Faster constants) | **Optimized** |

### 🔑 Key Knowledge

* **Pre-allocation:** If you know exactly how big your result needs to be (here, it's `nums.length`), always create an array of that size immediately. It avoids the computer having to "guess and resize" memory.
* **Pointer Arithmetic:** Increasing an index by 2 (`index += 2`) is a common way to stay on Even or Odd tracks within a single loop.

