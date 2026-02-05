
# 🔄 Rotate Image | Matrix Rotation Strategy

## Intuition
The problem asks us to rotate an `n x n` 2D matrix by **90 degrees clockwise** in-place.

Attempting to move cells directly to their final 90-degree position is complex because it involves a 4-way swap that can be hard to track. Instead, we can break the rotation down into two simpler, standard matrix operations:

1.  **Transpose:** Convert rows into columns. This aligns the data diagonally.
2.  **Reflect (Reverse):** Flip the matrix horizontally. This moves the columns to their correct rotated position.

**Formula:** `Rotate 90° Clockwise = Transpose + Reverse Rows`

## Approach

### Step 1: Transpose the Matrix
We swap elements across the main diagonal (top-left to bottom-right).
* Swap `matrix[i][j]` with `matrix[j][i]`.
* **Note:** We only iterate the upper triangle (`j starts at i + 1`) to avoid swapping the same elements twice.

### Step 2: Reverse Each Row
After transposing, the first column is now the first row, but the elements are in reverse order compared to a 90-degree rotation.
* We iterate through every row and reverse it using a standard two-pointer approach (`left` and `right`).

---

## Visual Example (3x3)

**1. Original:**
```text
[ 1, 2, 3 ]
[ 4, 5, 6 ]
[ 7, 8, 9 ]

```

**2. After Transpose (Swap `(i,j)` with `(j,i)`):**
*Row 0 (`1,2,3`) becomes Col 0.*

```text
[ 1, 4, 7 ]
[ 2, 5, 8 ]
[ 3, 6, 9 ]

```

**3. After Reverse (Reverse each row):**
*Row 0 `[1, 4, 7]` becomes `[7, 4, 1]`.*

```text
[ 7, 4, 1 ]
[ 8, 5, 2 ]
[ 9, 6, 3 ]

```

*(This is the correct 90° clockwise rotation!)*

---

## Complexity Analysis

* **Time Complexity:** `O(N^2)`
* Transposing visits roughly `N*N/2` elements.
* Reversing visits `N*N` elements.
* Total is proportional to the number of cells in the grid.


* **Space Complexity:** `O(1)`
* We modify the matrix **in-place** without using any extra data structures.



## Java Code

```java
class Solution {
    // Helper function to reverse a 1D array
    public void reverse(int[] arr) {
        int l = 0;
        int r = arr.length - 1;
        while (l < r) {
            int temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            l++;
            r--;
        }
    }

    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // Step 1: Transpose the matrix
        // (Convert rows to columns)
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse each row
        // (Flip horizontally to achieve clockwise rotation)
        for (int i = 0; i < n; i++) {
            reverse(matrix[i]);
        }
    }
}

```
