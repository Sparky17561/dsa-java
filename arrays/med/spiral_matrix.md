# 🌀 Spiral Matrix Traversal | Layer-by-Layer Boundary Processing

## Intuition
This problem asks us to traverse a matrix in a spiral order: **Right → Down → Left → Up**, and then repeat this pattern for inner layers. 

We maintain four dynamic boundaries (`top`, `bottom`, `left`, `right`) that define the current "active" layer of the matrix. As we traverse each side, we shrink the corresponding boundary inward to ensure we never visit those elements again. The key challenge is handling edge cases (like non-square matrices) where a row or column might be exhausted before a full spiral cycle completes.

## Approach
We use a **Boundary-Shrinking Strategy**:

1.  **Boundary Initialization:** * `top = 0`, `bottom = rows - 1`
    * `left = 0`, `right = cols - 1`

2.  **Traversal Loop:** (Runs while `top <= bottom` and `left <= right`)

    * **Step 1 (Right):** Traverse from `left` to `right` along the `top` row.
        * *Action:* Increment `top++` (Top row is done).
        
    * **Step 2 (Down):** Traverse from `top` to `bottom` along the `right` column.
        * *Action:* Decrement `right--` (Right column is done).
        
    * **Step 3 (Left):** Check if `top <= bottom` (to avoid double-counting in a single row). 
        * Traverse from `right` to `left` along the `bottom` row.
        * *Action:* Decrement `bottom--`.
        
    * **Step 4 (Up):** Check if `left <= right` (to avoid double-counting in a single column).
        * Traverse from `bottom` to `top` along the `left` column.
        * *Action:* Increment `left++`.

3.  **Completion:** The loop terminates when the boundaries cross, meaning all layers have been visited.



## Complexity Analysis

* **Time Complexity:** `O(m × n)`  
    We visit every element in the matrix exactly once, where `m` is the number of rows and `n` is the number of columns.

* **Space Complexity:** `O(1)`  
    Excluding the output list `spiral`, we only use a constant amount of extra space for the boundary variables (`top`, `bottom`, `left`, `right`).

## Java Code

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int bottom = matrix.length - 1;
        int right = matrix[0].length - 1;
        int left = 0;
        int top = 0;
        
        ArrayList<Integer> spiral = new ArrayList<>();
        
        while (top <= bottom && left <= right) {
            
            // 1. Move Right
            for (int i = left; i <= right; i++) {
                spiral.add(matrix[top][i]);
            }
            top++; // Top row is processed, move boundary down

            // 2. Move Down
            for (int j = top; j <= bottom; j++) {
                spiral.add(matrix[j][right]);
            }
            right--; // Right column is processed, move boundary left

            // 3. Move Left
            // Check if there is still a valid row remaining
            if (top <= bottom) {
                for (int k = right; k >= left; k--) {
                    spiral.add(matrix[bottom][k]);
                }
                bottom--; // Bottom row is processed, move boundary up
            }

            // 4. Move Up
            // Check if there is still a valid column remaining
            if (left <= right) {
                for (int l = bottom; l >= top; l--) {
                    spiral.add(matrix[l][left]);
                }
                left++; // Left column is processed, move boundary right
            }
        }

        return spiral;
    }
}