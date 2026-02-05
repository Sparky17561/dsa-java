# ⬛ Set Matrix Zeroes | In-Place Optimization

## Intuition
The naive approach to this problem requires making a copy of the matrix ($O(M \times N)$ space) or keeping separate arrays for rows and columns ($O(M + N)$ space) to track which ones need to be zeroed.

To optimize to **$O(1)$ space**, we use the **first row** and **first column** of the matrix itself as our "checklist."
* If `matrix[i][j]` is `0`, we mark `matrix[i][0]` (Row Header) and `matrix[0][j]` (Column Header) as `0`.
* **Conflict:** Since `matrix[0][0]` belongs to both the first row and first column, we use a separate variable `col0` to track the status of the first column independently.



## Approach

### Step 1: The "Survey" (Marking Phase)
We iterate through the matrix to find zeros.
* If we find a `0` at `(i, j)`, we set the **Row Header** `matrix[i][0]` to `0` and the **Column Header** `matrix[0][j]` to `0`.
* **Special Case:** If any zero is found in the **0th column** (where `j=0`), we set our separate flag `col0 = 0`.

### Step 2: Zero the Inner Matrix
We iterate through the inner matrix (starting from `row 1, col 1`).
* For every cell `(i, j)`, check its headers:
    * Is `matrix[i][0] == 0`? (Row is marked)
    * OR Is `matrix[0][j] == 0`? (Column is marked)
* If either is true, set `matrix[i][j] = 0`.

### Step 3: Handle the First Row
Check `matrix[0][0]`. If it is `0`, it means the first row originally contained a zero (or a zero was projected onto it). We zero out the entire first row.

### Step 4: Handle the First Column
Check the `col0` flag. If it is `0`, it means the first column originally contained a zero. We zero out the entire first column.

---

## Complexity Analysis

* **Time Complexity:** $O(M \times N)$
    * We traverse the entire matrix twice (once to mark, once to set zeros).
* **Space Complexity:** $O(1)$
    * We do not use any extra arrays. The `col0` variable uses constant extra space.

---

## Java Code

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int n = matrix.length;      // Rows
        int m = matrix[0].length;   // Columns
        int col0 = 1;               // Flag for the 0th Column

        // Step 1: Traverse and Mark Headers
        for (int i = 0; i < n; i++) {
            // Check if 0th column needs to be zeroed
            if (matrix[i][0] == 0) col0 = 0;

            // Check the rest of the columns (1 to m-1)
            for (int j = 1; j < m; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0; // Mark Row Header
                    matrix[0][j] = 0; // Mark Col Header
                }
            }
        }

        // Step 2: Fill Inner Matrix (1 to n-1, 1 to m-1)
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                // If either header is 0, set cell to 0
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Step 3: Handle First Row
        // matrix[0][0] acts as the flag for the 0th row
        if (matrix[0][0] == 0) {
            for (int j = 0; j < m; j++) {
                matrix[0][j] = 0;
            }
        }

        // Step 4: Handle First Column
        // col0 acts as the flag for the 0th column
        if (col0 == 0) {
            for (int i = 0; i < n; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}