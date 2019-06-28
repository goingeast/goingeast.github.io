## Description
>Given an array A of 0s and 1s, we may change up to K values from 0 to 1.
>Return the length of the longest (contiguous) subarray that contains only 1s. 

>Example 1:
Input: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
Output: 6
Explanation: 
[1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
>
>Example 2:
Input: A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
Output: 10
Explanation: 
[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
> 
>Note:
1 <= A.length <= 20000
0 <= K <= A.length
A[i] is 0 or 1 

## Solution
We can think this problem in another way. Lets use classic sliding window template in the [thread](strstr.io)

## Code
```cpp
class Solution {
public:
    int longestOnes(vector<int>& A, int K) {
        int maxLength = 0;
        int left = 0;
        int count = 0;
        for(int i = 0; i < A.size(); ++i) {
            if(A[i] == 0) {                          /*❶*/
                count++;
            }
            while(count > K) {                       /*❷*/
                if(A[left] == 0){
                    count--;
                }
                left++;
            }
            maxLength = max(maxLength, i - left + 1);/*❸*/
        }
        return maxLength;
    }
};
```
❶ update count, it is related to K.  
❷ move left bound of window and update the count.  
❸ update the length of window.  

## Insight
There are lots of questions can be solved by similar way. And sliding window technique is very popular approach.
