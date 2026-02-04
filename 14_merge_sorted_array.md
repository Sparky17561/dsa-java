Here is your concise Revision Note for the Merge Sorted Array problem.🔄 Merge Sorted ArrayGoalMerge two sorted arrays (nums1 and nums2) into nums1 as a single sorted array.📊 ComplexityTime Complexity: $O(M + N)$We iterate through both arrays once from back to front.Space Complexity: $O(1)$In-place operation. We use the empty space at the end of nums1.💻 Code ImplementationJavaclass Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1;      // Pointer for end of valid nums1
        int j = n - 1;      // Pointer for end of nums2
        int k = m + n - 1;  // Pointer for very end of nums1 (buffer)

        // Compare and fill from the BACK
        while (i >= 0 && j >= 0) {
            if (nums1[i] >= nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }

        // Handle leftovers from nums2
        // If nums1 has leftovers, they are already in place!
        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
}
🧠 Key Logic to RememberReverse Filling:Start filling from the end (k = m + n - 1) to avoid overwriting elements in nums1 that haven't been processed yet.The Three Pointers:i tracks the largest unused element in nums1.j tracks the largest unused element in nums2.k tracks the current fill position.The "Leftover" Rule:If nums2 runs out first (j < 0), we are done. The remaining elements of nums1 are already in their correct sorted positions.If nums1 runs out first (i < 0), we must copy the remaining elements of nums2 into nums1.