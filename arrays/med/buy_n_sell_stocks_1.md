# Best Time to Buy and Sell Stock (Java Solution)

### 📖 Problem Overview

You are given an array of prices where `prices[i]` is the stock price on the  day. You want to maximize your profit by choosing **one day** to buy and a **different day in the future** to sell.

### 💡 The Core Logic (The "Aha!" Moment)

Instead of comparing every possible pair of days (which is slow), we use a **Greedy Approach** in a single pass.

Imagine you are walking through time. As you go, you only care about two things:

1. **What is the lowest price I have seen *so far*?** (This is your potential "Buy" price).
2. **If I sold today, is this the best profit I've seen *so far*?**

### ⚡ Step-by-Step Execution

1. **Initialize:** Start by assuming the first day is the cheapest (`smallest = 0`). Set your maximum profit (`max`) to a very low number.
2. **Iterate:** Walk through the prices starting from Day 1.
3. **Decision (The `if/else` block):**
* **Case A:** Is the current price *lower* than the price at my `smallest` index?
* **Action:** Update `smallest`. We found a new "valley." We don't sell now; we just note that this is a better buying opportunity for future days.


* **Case B:** Is the current price *higher* than my `smallest` price?
* **Action:** Calculate the profit (`current price - prices[smallest]`). If this profit is higher than our previous record (`max`), save it.





### 🔑 Key Knowledge & Concepts used

To write or understand this solution, you need to know:

* **Greedy Algorithm:** The strategy of making the locally optimal choice at each stage (picking the lowest price seen so far) with the hope of finding a global optimum.
* **One-Pass Traversal:** Solving the problem by looking at each element only once, resulting in ** Time Complexity** (very fast).
* **Integer Limits:** Using `Integer.MIN_VALUE` ensures that any valid profit calculation will overwrite the initial value.
* **Indices vs Values:** The code tracks the `smallest` as an *index* (`int smallest = 0`), which is then used to access the value (`prices[smallest]`).

### 📊 Complexity Analysis

| Metric | Complexity | Explanation |
| --- | --- | --- |
| **Time** | **** | We iterate through the `prices` array exactly once. |
| **Space** | **** | We only use variables (`smallest`, `diff`, `max`) to store state; no extra arrays are created. |

---

### 📝 Logic Flow Example

Input: `[7, 1, 5, 3, 6, 4]`

1. **Day 0 (7):** Start. `smallest` points here.
2. **Day 1 (1):** Is `1 < 7`? **Yes.** Update `smallest` to point here. (New low found).
3. **Day 2 (5):** Is `5 < 1`? **No.** Profit = `5 - 1 = 4`. `max` becomes 4.
4. **Day 3 (3):** Is `3 < 1`? **No.** Profit = `3 - 1 = 2`. `max` stays 4.
5. **Day 4 (6):** Is `6 < 1`? **No.** Profit = `6 - 1 = 5`. **`max` becomes 5.**
6. **Day 5 (4):** Is `4 < 1`? **No.** Profit = `4 - 1 = 3`. `max` stays 5.

**Result:** 5.
