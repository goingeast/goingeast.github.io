---
categories: Leetcode
tags: binarySearch
---
## Description
>A peak element is an element that is greater than its neighbors.
>
>Given an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index.
>
>The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.
>
>You may imagine that nums[-1] = nums[n] = -∞.
>
>Example 1:
>
>Input: nums = [1,2,3,1]
>Output: 2
>Explanation: 3 is a peak element and your function should return the index number 2.
>
>Example 2:
>
>Input: nums = [1,2,1,3,5,6,4]
>Output: 1 or 5 
>Explanation: Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
>
>Note:
>Your solution should be in logarithmic complexity.

## Solution
Use binary search, the data can be considered partial sorted. There could be a couple of peaks. And also we need find the lower bound of the peak. so we use the lower bound binary search template in this [summary](https://strstr.io/Binary-Search/).
## Code
``` cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int left = 0;
        int right = nums.size() -1;
        while(left < right){                    /*❶*/
            int mid = left + (right - left)/2;
            if(nums[mid] >= nums[mid+1]){       /*❷*/
                right = mid;                    /*❷*/
            }else {
                left = mid+1;
            }
        }
        return left;
    }
};
```
❶, ❷: all are key attributes of lower bound binary search template.

## Insight
This question is the second kind of question in the [summary](https://strstr.io/Binary-Search/), data is somehow partially sorted, but we can still leverage it by using binary search.
