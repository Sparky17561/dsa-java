# 🦄 Single Number | Bit Manipulation (XOR)

## Intuition
The problem asks us to find the **single element** that appears only once in an array where every other element appears **twice**.

We could use a Hash Map to count frequencies ($O(N)$ space), but we can solve this with **$O(1)$ space** using the properties of the **XOR** bitwise operation.

### The Magic of XOR (`^`)
1.  **Identity:** $a \oplus 0 = a$
2.  **Self-Inverse:** $a \oplus a = 0$
3.  **Commutative:** The order doesn't matter ($a \oplus b \oplus a = a \oplus a \oplus b = 0 \oplus b = b$).

## Approach
We initialize a variable `res = 0`. We iterate through the array and XOR every number with `res`.
* All the numbers that appear twice will XOR with themselves and become `0` (canceling each other out).
* The only number remaining in `res` at the end will be the single number that didn't get canceled.



### Trace Example
**Input:** `[4, 1, 2, 1, 2]`
* `0 ^ 4 = 4`
* `4 ^ 1`
* `4 ^ 1 ^ 2`
* `4 ^ 1 ^ 2 ^ 1` $\rightarrow$ (Rearrange: `4 ^ (1 ^ 1) ^ 2` $\rightarrow$ `4 ^ 0 ^ 2`)
* `4 ^ 0 ^ 2 ^ 2` $\rightarrow$ (Rearrange: `4 ^ 0 ^ (2 ^ 2)` $\rightarrow$ `4 ^ 0 ^ 0`)
* **Result:** `4`

---

## Complexity Analysis

* **Time Complexity:** $O(N)$
    * We iterate through the array exactly once.
* **Space Complexity:** $O(1)$
    * We use only one variable `res`.

---

## Java Code

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0; // 0 is the identity element for XOR
        
        for (int n : nums) {
            res ^= n; // XOR effectively toggles bits on and off
        }

        return res;
    }
}