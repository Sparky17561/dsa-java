
# Leaders in an Array (Java Solution)

### 📖 Problem Overview

You need to find all the **"Leaders"** in an array.
An element is a **Leader** if it is greater than or equal to **all** the elements to its right side.

* **Note:** The rightmost element is *always* a leader because there is nothing to its right.

### 💡 The Core Logic (Right-to-Left Scan)

Instead of checking every element against all elements to its right (which would be slow ), we iterate **backwards**.

**The Strategy:**

1. Start from the very last element. This is your first "Maximum".
2. Walk backwards (right to left).
3. Ask: **"Is the current number bigger than (or equal to) the biggest number I've seen so far?"**
* **Yes:** It's a leader. Update the "Maximum" and save it.
* **No:** It's smaller than something to its right. Ignore it.



### ⚡ Step-by-Step Trace

Input: `[16, 17, 4, 3, 5, 2]`

1. **Start at End (Index 5):** Value `2`.
* It's the first element. Max = `2`. List = `[2]`.


2. **Index 4:** Value `5`.
* Is `5 >= 2`? **Yes.**
* Max = `5`. List = `[2, 5]`.


3. **Index 3:** Value `3`.
* Is `3 >= 5`? **No.** (Skip).


4. **Index 2:** Value `4`.
* Is `4 >= 5`? **No.** (Skip).


5. **Index 1:** Value `17`.
* Is `17 >= 5`? **Yes.**
* Max = `17`. List = `[2, 5, 17]`.


6. **Index 0:** Value `16`.
* Is `16 >= 17`? **No.** (Skip).



**Result:** `[2, 5, 17]`
**Reverse it:** `[17, 5, 2]` (Final Answer).

### 🔑 Key Knowledge & Concepts

* **Reverse Iteration:** Iterating backwards allows us to solve this in **one pass** () because we carry the "required knowledge" (the current maximum) with us as we move.
* **Greedy Property:** We only care about the *immediate* maximum. We don't need to know the entire history of the array, just the biggest thing seen "so far" from the right.
* **`Collections.reverse()`:** Since we find the rightmost leaders first, our list is built backwards (`[2, 5, 17]`). We must reverse it at the end to match the array order.

### 📊 Complexity Analysis

| Metric | Complexity | Explanation |
| --- | --- | --- |
| **Time** | **** | We iterate through the array exactly once. |
| **Space** | **** | We use a list to store the output. |

---

### 🚀 Next Step

This is a standard interview problem. The "backward pass" technique is also useful for problems like **"Daily Temperatures"** or **"Next Greater Element"**.
