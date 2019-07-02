## Description
>Given a 32-bit signed integer, reverse digits of an integer.
>
>Example 1:
Input: 123
Output: 321
>
>Example 2:
Input: -123
Output: -321
>
>Example 3:
Input: 120
Output: 21
>
>Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Solution
Use the typical way to get last digit of a number and shift the digit to most significant position. like,
```cpp
int ret = 0;
while(x) {
    int remain = x % 10;
    ...
    ret = ret * 10 + remain;
    x /= 10;
} 
```
However, all the number conversion stuff needs to pay a attention about overflow. For a integer, the range is from -2147483648 to 2147483627. And we usually use this formula:   
$$ret > (INT_{MAX})/10 \lor (ret = (INT_{max}) /10 \land remain > 7) $$
$$ret < (INT_{MIN})/10 \lor (ret = (INT_{MIN}) /10 \land remain < -8) $$

## Code
```cpp
class Solution {
public:
    int reverse(int x) {
        int ret = 0;
        while(x) {
            int remain = x % 10;
            if(ret > INT_MAX/10 || ret < INT_MIN/10) return 0;  /*❶*/
            /* if x is string, we need the second condition*/   /*❷*/
            /* if(ret > INT_MAX/10 || (ret == INT_MAX/10 && remain > 7) ||
                ret < INT_MIN/10 || (ret == INT_MIN/10 && remain < -8)) {
                    return 0;
            } */
            ret = ret * 10 + remain;
            x /= 10;
        }
        return ret;
    }
};
```
❶ As the input is integer, if the last digit is not 0, 1, 2, this is impossible to meet the condition (ret == INT_MAX/10 && remain > 7 or (ret == INT_MIN/10 && remain < -8)). So we can only use first set of condition.  
❷ As the inpur is string, there could be other numbers beside 0, 1, 2.
