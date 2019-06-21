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
    
    while(left <= right) {                         /*❶*/
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

These four keys are very important. ALL other questions are evolved from it.  

## How to solve problems using BS  
