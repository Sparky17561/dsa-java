# Remove Outer Parentheses (Java)

## Problem Statement

Given a valid parentheses string `s`, remove the **outermost parentheses of every primitive substring** and return the resulting string.

A **primitive valid parentheses string** is a non-empty substring that cannot be split into smaller valid parentheses strings.

This problem commonly appears on coding practice platforms such as LeetCode.

---

## Example

### Example 1

**Input**

```
s = "(()())(())"
```

**Output**

```
"()()()"
```

**Explanation**

```
(()()) → remove outer parentheses → ()()
(())   → remove outer parentheses → ()
```

Final result:

```
()()()
```

---

### Example 2

**Input**

```
s = "(()())(())(()(()))"
```

**Output**

```
"()()()()(())"
```

---

## Approach

The key idea is to **track the number of open parentheses** using a counter.

* When encountering `'('`, increment the counter.
* When encountering `')'`, decrement the counter.
* Only append parentheses to the result **if they are not the outermost ones**.

### Key Logic

* The **first `(` of a primitive substring** should not be added.
* The **last `)` of a primitive substring** should not be added.

This ensures that only **inner parentheses** remain.

---

## Algorithm

1. Convert the string into a character array.
2. Use a counter `open` to track open parentheses.
3. Traverse the string from index `1` to the end.
4. If the current character is `'('`:

   * Increment `open`
   * If `open > 1`, append `'('` to the result
5. If the current character is `')'`:

   * If `open > 1`, append `')'`
   * Decrement `open`
6. Return the final string.

---

## Java Implementation

```java
class Solution {
    public String removeOuterParentheses(String s) {
        int len = s.length();
        if (len <= 2) return "";

        char[] c = s.toCharArray();
        StringBuilder newString = new StringBuilder();

        int open = 1;

        for (int i = 1; i < len; i++) {

            if (c[i] == '(') {
                open++;

                if (open > 1) {
                    newString.append('(');
                }
            } 
            else {
                if (open > 1) {
                    newString.append(')');
                }

                open--;
            }
        }

        return newString.toString();
    }
}
```

---

## Dry Run

Input:

```
s = "(()())"
```

| Index | Character | Open Count | Action     |
| ----- | --------- | ---------- | ---------- |
| 0     | (         | 1          | Skip outer |
| 1     | (         | 2          | Append '(' |
| 2     | )         | 1          | Append ')' |
| 3     | (         | 2          | Append '(' |
| 4     | )         | 1          | Append ')' |
| 5     | )         | 0          | Skip outer |

Result:

```
()()
```

---

## Complexity Analysis

### Time Complexity

```
O(n)
```

We traverse the string once.

### Space Complexity

```
O(n)
```

A `StringBuilder` is used to store the resulting string.

---

## Key Concepts Used

* String Traversal
* Parentheses Matching
* Counter Tracking
* StringBuilder for efficient string construction

---

## Summary

This solution efficiently removes outermost parentheses by:

* Maintaining a **counter of open parentheses**
* Adding only **inner parentheses** to the result
* Traversing the string **once**

This makes the algorithm **linear time and space efficient**.
