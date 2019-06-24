## Description
>Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
>
>(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).
>
>Find the minimum element.
>
>You may assume no duplicate exists in the array.
>
>Example 1:
Input: [3,4,5,1,2] 
Output: 1
>
>Example 2:
Input: [4,5,6,7,0,1,2]
Output: 0

## Solution
Use lower bound template described in the [summary](https://strstr.io/Binary-Search/). Also this question belongs to the second type of binary search question whose data is partially sorted. We have to find a way to eliminate half part of data.

## Code
```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;

        while(left < right){
            int mid = left + (right -left)/2;
            if(nums[mid] < nums[right]){       /*❶*/
                right = mid;
            } else if(nums[mid] > nums[right]) {
                left = mid + 1;
            }
        }
        return nums[left];                     /*❷*/
    }
};
```
❶ it means the part [mid, right] is sorted and we are sure the smallest element is in [left, mid], also there is no duplication elements, we don't have to check if nums[mid] == nums[right].  
❷ return the lower bound element
