---
categories: Leetcode
---

## Introduction  
In this video, we gonna discuss binary search (BS) as below. 
- Typical use case of BS. 
- Key points of BS code
- How to solve problems using BS
- Examples
- Template code  

## Typical use case of binary search?  
Here is a quote from wikipedia:
> In computer science, binary search, also known as half-interval search, logarithmic search, or binary chop, is a search algorithm that finds the position of a target value within a sorted array. Binary search compares the target value to the middle element of the array. If they are not equal, the half in which the target cannot lie is eliminated and the search continues on the remaining half, again taking the middle element to compare to the target value, and repeating this until the target value is found. If the search ends with the remaining half being empty, the target is not in the array.

From the describtion above, we have to get three keys:
1. Data is **sorted**.
2. **Half of data is eliminated** due to missing some condition.
3. **Repeat** the process until **target is found** or **meet end condition**.  

## Key points of BS code  
With the three key points in mind, let see how our code implements these.

``` cpp
int binarySearch(vector<int>& sortedIncreasingData, int target) {
    int left = 0;
    int right = sortedData.size() - 1;
    
    while(left <= right) {                     /*❶*/
      int mid = left + (right - left) / 2;
      if(sortedData[mid] == target) {          /*❷*/
          return mid;
      } else if(sortedData[mid] < target) {    /*❸*/
          left = mid + 1;                      /*❹*/
      } else {
          right = mid - 1;                     /*❹*/
      }
      }
    return -1;
}
```

① End condition: when left index  and right index are **crossed**.  
② Find target.  
③ Condition to eliminate a half data.  
④ Move left or right index,  so that the data at mid index can move close to target. Quiz: why mid + 1 or mid - 1, why not mid?

Variant 1
Find lower bound element to meet the condition. eg. [Leetcode162 Find Peak Element](https://strstr.io/Leetcode162-Find-Peak-Element/)
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
Variant 2
Adding post processing of the condidates at index left and right. eg. [Closest In Sorted Array](https://strstr.io/Closest-In-Sorted-Array/)
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

These four keys are very important. ALL other questions are evolved from it.  

## How to solve problems using BS
- [Easy] The input data is sorted obviously or can be sorted, and just need find the target within the requirement.
	- [Leetcode34 Find First and Last Position of Element in Sorted Array](www.strstr.io/)
	- [Leetcode35 Search Insert Position](www.strstr.io/)
	- [Leetcode74 Search a 2D Matrix](www.strstr.io/)
	- [Leetcode350 Intersection of Two Arrays II](www.strstr.io/)
	- [Leetcode167 Two Sum II - Input array is sorted](www.strstr.io/)
	- [Leetcode706 Binary Search](www.strstr.io)
	- [Leetcode278 First Bad Version](www.strstr.io)
	- [Leetcode702 Search in a Sorted Array of Unkown Size](www.strstr.io)  
	- [Leetcode1064 Fixed Point](https://strstr.io/Leetcode1064-Fixed-Point/)
- [Medium] The input data is partially sorted, we can use sorted part to decide to which half to eliminate
	- [Leetcode162 Find Peak Element](https://strstr.io/Leetcode162-Find-Peak-Element/)
	- [Leetcode852 Peak Index in a Mountain Array](https://strstr.io/Leetcode162-Find-Peak-Element/)
- [Medium] Need figure out a check function to decide to which half to eliminate.
	- [Leetcode1060 Missing Element in Sorted Array](https://strstr.io/Leetcode1060-Missing-Element-in-Sorted-Array/)
- [Hard] Use binary search to find a solution of problem, instead of brute force all the solution space.
	- [Leetcode875 Koko Eating Bananas](https://strstr.io/Leetcode875-Koko-Eating-Bananas/)
