🧮 Subarray Sum Equals K
Goal
Find the total number of continuous subarrays whose sum equals k.

📊 Complexity
Time Complexity: O(N)

We traverse the array exactly once. HashMap lookups are O(1) on average.

Space Complexity: O(N)

In the worst case (all prefix sums are unique), the map stores N entries.

💻 Code Implementation
Java
import java.util.HashMap;

class Solution {
    public int subarraySum(int[] nums, int k) {
        int currSum = 0;
        int count = 0;
        // Map stores <PrefixSum, Frequency>
        HashMap<Integer, Integer> map = new HashMap<>();
        
        // Base Case: A sum of 0 has appeared once (before the array starts)
        map.put(0, 1); 

        for (int num : nums) {
            currSum += num;
            int remaining = currSum - k;
            
            // 1. If (currSum - k) exists, it means we found valid subarrays
            if (map.containsKey(remaining)) {
                count += map.get(remaining);
            }
            
            // 2. Record the current prefix sum for future checks
            map.put(currSum, map.getOrDefault(currSum, 0) + 1);
        }
        
        return count;
    }
}
🧠 Key Logic to Remember
The Formula:

If PrefixSum[i] - PrefixSum[j] == k, then the subarray between j and i sums to k.

Rearranged: We look for PrefixSum[j] = CurrSum - k.

Why HashMap?

It stores how many times a specific prefix sum has occurred.

If currSum - k has appeared 3 times previously, it means there are 3 different subarrays ending at the current index that sum to k.

The Base Case:

map.put(0, 1) handles subarrays that start from index 0. If currSum itself becomes k, then currSum - k = 0, and we need that initial 1 to count it.