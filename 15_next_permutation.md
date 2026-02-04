🔄 Next PermutationGoalRearrange numbers into the lexicographically next greater permutation of numbers. If not possible (already largest), rearrange to the lowest possible order (sorted ascending).📊 ComplexityTime Complexity: $O(N)$We scan the array three times in the worst case (find break point, find swap candidate, reverse).Space Complexity: $O(1)$In-place modification.💻 Code ImplementationJavaclass Solution {
    // Helper to reverse array from index l to r
    public void reverse(int[] nums, int l, int r) {
        while (l < r) {
            int temp = nums[l];
            nums[l++] = nums[r];
            nums[r--] = temp;
        }
    }

    public void nextPermutation(int[] nums) {
        int n = nums.length;
        int i = n - 1;

        // 1. Find the first decreasing element from the right (the "pivot")
        // We look for the first index i where nums[i-1] < nums[i]
        while (i > 0 && nums[i - 1] >= nums[i]) {
            i--;
        }

        // Case: Array is purely descending (e.g., 3, 2, 1) -> Reverse whole array
        if (i == 0) {
            reverse(nums, 0, n - 1);
            return;
        }

        // 2. Find the smallest element > pivot from the right
        int j = n - 1;
        while (j >= i && nums[j] <= nums[i - 1]) {
            j--;
        }

        // 3. Swap the pivot with that element
        int temp = nums[i - 1];
        nums[i - 1] = nums[j];
        nums[j] = temp;

        // 4. Reverse the suffix (everything after the pivot index)
        reverse(nums, i, n - 1);
    }
}
🧠 Key Logic to RememberThe "Pivot" Concept:Traverse from the back to find the first number that breaks the descending order (nums[i-1] < nums[i]). This is where the permutation can be "incremented".The "Next Greater" Swap:We can't just swap with any number. We must swap with the smallest number on the right that is larger than our pivot to get the immediate next permutation.Minimize the Tail:After swapping, the suffix (right side) is still in descending order (largest possible). To make it the smallest possible suffix for the new prefix, we reverse it.