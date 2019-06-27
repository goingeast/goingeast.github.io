## Description
>Given an array of integers, return indices of the two numbers such that they add up to a specific target.
>
>You may assume that each input would have exactly one solution, and you may not use the same element twice.
>
>Example:
>Given nums = [2, 7, 11, 15], target = 9,
>Because nums[0] + nums[1] = 2 + 7 = 9,
>return [0, 1].

## Solution
1. Sorted the array, then use [two pointers](strstr.io).
2. Iterative, for nums[i], use [hashmap](strstr.io) to check if we've already had a value (target - nums[i]).

## Code

``` cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // sort or hashmap
        unordered_map<int, int> index;
        for(int i = 0; i < nums.size(); ++i) {
            if(index.count(target - nums[i])) {
                return {i , index[target - nums[i]]};
            } else {
                index[nums[i]] = i;
            }
        }
        return {-1, -1};
    }
};
```
