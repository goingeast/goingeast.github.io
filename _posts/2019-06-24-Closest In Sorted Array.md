
## Description
>Given a target integer T and an integer array A sorted in ascending order, find the index i in A such that A[i] is closest to T.
>
>Assumptions
>There can be duplicate elements in the array, and we can return any of the indices with same value.
>
>Examples
>
>A = {1, 2, 3}, T = 2, return 1  
A = {1, 4, 6}, T = 3, return 1  
A = {1, 4, 6}, T = 5, return 1 or 2  
A = {1, 3, 3, 4}, T = 2, return 0 or 1 or 2  

## Solution

Using binary search, we need post processing to decide which element is closet to target.

## code

``` cpp
class Solution {
 public:
  int solve(vector<int> input, int target) {
    if(input.size() == 0)
      return -1;
    
    int left = 0;
    int right = input.size() -1;
    
    while(left < right -1){            /*❶*/
      int mid = (right+left)/2;
      if(target == input[mid]){
        return mid;
      }else if(target > input[mid]){
        left = mid;                   /*❷*/
      }else{
        right = mid;
      }
    }
    // post processing.               /*❸*/
    if(abs(input[left] - target) < abs(input[right] - target)){
      return left;
    }else{
      return right;
    }
  }
};
```
