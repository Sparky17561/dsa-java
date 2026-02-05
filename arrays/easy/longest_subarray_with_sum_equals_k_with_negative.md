# Longest Subarray with Sum K (HashMap / Prefix Sum)

## Description
This solution finds the length of the longest subarray that sums to `k` using a **HashMap** to store **Prefix Sums**. This is the universal solution that correctly handles arrays containing **negative numbers**.

## Algorithm
1.  **Prefix Sum:** Iterate through the array, maintaining a running `sum`.
2.  **The Math:** To find a subarray ending at index `i` with sum `k`, we look for an earlier prefix sum equal to `sum - k`.
    * `CurrentPrefixSum - OldPrefixSum = Target (k)`
    * `OldPrefixSum = CurrentPrefixSum - k`
3.  **Lookup:** Check if `sum - k` exists in the HashMap. If yes, the subarray between that old index and the current index has sum `k`.
4.  **Store:** Save the `sum` and its index `i` in the map (only if it's not already there, to preserve the longest possible length).

## Key Edge Cases
* **Subarray starting at 0:** We initialize the map with `{0, -1}`. This handles cases where the subarray starts from the very beginning of the array.
* **Negative Numbers:** Works perfectly because it relies on math rather than the monotonic growth of the sum.

## Complexity
* **Time Complexity:** $O(N)$ - One pass through the array with $O(1)$ map lookups.
* **Space Complexity:** $O(N)$ - Stores up to $N$ entries in the HashMap.

## Java Implementation
```java
import java.util.HashMap;

class Solution {
    public int longestSubarray(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap<>();
        int maxLen = 0;
        int sum = 0;
        int remaining = 0;

        // Base case: Sum 0 exists at index -1
        map.put(0, -1);

        for(int i = 0; i < nums.length; i++){
            sum += nums[i];
            
            // Formula: OldPrefix = CurrentSum - Target
            remaining = sum - k; 

            // Check if we have seen the required prefix sum before
            if(map.containsKey(remaining)){
                maxLen = Math.max(maxLen, i - map.get(remaining));
            }

            // Only add sum if it's new (to keep the leftmost index for max length)
            if(!map.containsKey(sum)){
                map.put(sum, i);
            }
        }
        return maxLen;
    }
}