---
categories: Leetcode
tags: binary-search
---

## Description
>Koko loves to eat bananas.  There are N piles of bananas, the i-th pile has piles[i] bananas.  The guards have gone and will come back in H hours.
>
>Koko can decide her bananas-per-hour eating speed of K.  Each hour, she chooses some pile of bananas, and eats K bananas from that pile.  If the pile has less than K bananas, she eats all of them instead, and won't eat any more bananas during this hour.
>
>Koko likes to eat slowly, but still wants to finish eating all the bananas before the guards come back.
>
>Return the minimum integer K such that she can eat all the bananas within H hours.
>
>Example 1:
>Input: piles = [3,6,7,11], H = 8
Output: 4
>
>Example 2:
Input: piles = [30,11,23,4,20], H = 5
Output: 30
>
>Example 3:
Input: piles = [30,11,23,4,20], H = 6
Output: 23
> 
>Note:
>
>1 <= piles.length <= 10^4
piles.length <= H <= 10^9
1 <= piles[i] <= 10^9

## Solution
Use binary search, this problem is the fourth kind of question in our binary search problem set in this [summary](https://strstr.io/Binary-Search/). When we want to find a target that meets certain conditions in a large or limited solution space, we should think of if we can use binary search, eg. Find square root of a number.

## Code
``` cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int H) {
        int left = 1;
        int right = maxPile(piles);             /*❶*/
        
        while(left < right) {                   /*❷*/
            int mid = left + (right - left)/2;
            if(canEat(piles, mid, H)) {
                right = mid;
            }else{
                left = mid + 1;
            }
        }
        return left;                           /*❸*/
    }
    
    int maxPile(vector<int>& piles) {
        int max = 0;
        for(auto pile : piles) {
            if(max < pile) {
                max = pile;
            }
        }
        return max;
    }
    
    bool canEat(vector<int>& piles, int mid, int H) {
        int count = 0;
        for(auto pile : piles) {
            count += (pile-1)/mid + 1;
        }
        return count <= H;
    }
};
```
❶ Get the limited solution space, or we could just a very large space.  
❷, ❸ This is the template used in this [thread](https://strstr.io/Leetcode1060-Missing-Element-in-Sorted-Array/)

## Insight
- We can think of this question as is there a lower bound of H that meets the requirement. So when we want to find a lower bound of the target, use this template. and the index left is the lower bound position.
- After realize this is a template for looking for lower bound, please think of the reason why **left < right** and **right = mid**. These two key attributes are important.
