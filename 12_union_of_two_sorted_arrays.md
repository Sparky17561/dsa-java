🔗 Union of Two Sorted Arrays
Goal
Merge two sorted arrays into a single sorted array containing unique elements (no duplicates).

📊 Complexity
Time Complexity: O(N+M)

Single pass through both arrays (N and M).

Space Complexity: O(N+M)

To store the result array.

💻 Code Implementation
Java
import java.util.*;

class Solution {
    public int[] unionArray(int[] nums1, int[] nums2) {
        int i = 0, j = 0, k = 0;
        int n = nums1.length;
        int m = nums2.length;
        int[] res = new int[n + m]; // Max possible size

        // Two Pointers Loop
        while (i < n && j < m) {
            // Case 1: nums1 is smaller
            if (nums1[i] < nums2[j]) {
                if (k == 0 || res[k - 1] != nums1[i]) { // Deduplicate
                    res[k++] = nums1[i];
                }
                i++;
            } 
            // Case 2: nums2 is smaller
            else if (nums1[i] > nums2[j]) {
                if (k == 0 || res[k - 1] != nums2[j]) { // Deduplicate
                    res[k++] = nums2[j];
                }
                j++;
            } 
            // Case 3: Both are equal (add one, skip both)
            else {
                if (k == 0 || res[k - 1] != nums1[i]) { // Deduplicate
                    res[k++] = nums1[i];
                }
                i++;
                j++;
            }
        }

        // Handle Leftovers from nums1
        while (i < n) {
            if (k == 0 || res[k - 1] != nums1[i]) {
                res[k++] = nums1[i];
            }
            i++;
        }

        // Handle Leftovers from nums2
        while (j < m) {
            if (k == 0 || res[k - 1] != nums2[j]) {
                res[k++] = nums2[j];
            }
            j++;
        }

        // Return only the valid filled part
        return Arrays.copyOf(res, k);
    }
}
🧠 Key Logic to Remember
Pointers: i for nums1, j for nums2, k for result.

Comparison: Always pick the smaller element to keep it sorted.

Equality Case: If nums1[i] == nums2[j], add once and increment both i and j.

Deduplication Check: if (k == 0 || res[k-1] != val) ensures we never add the same number twice.