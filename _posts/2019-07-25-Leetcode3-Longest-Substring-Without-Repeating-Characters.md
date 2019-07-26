---
categories: Leetcode
tags: F
---

## Description

> Given a string, find the length of the longest substring without
> repeating characters.
> 
> Example 1:
> 
> Input: "abcabcbb" Output: 3  Explanation: The answer is "abc", with
> the length of 3.  Example 2:
> 
> Input: "bbbbb" Output: 1 Explanation: The answer is "b", with the
> length of 1. Example 3:
> 
> Input: "pwwkew" Output: 3 Explanation: The answer is "wke", with the
> length of 3.   
> Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Solution
This is the classic sliding window problem. we can use our sliding window template. Please review [Leetcode 76 Minimun Window Substring](https://strstr.io/Leetcode76-Minimum-Window-Substring/).

## Code
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int left = 0, ans = 0;
        int count = 0;                    /*❶*/
        unordered_map<char, int> map;
        for(int r = 0; r < s.size(); ++r){
            if(++map[s[r]] > 1) {         /*❷*/
                count++;
            }
            while(count > 0) {            /*❸*/
                if(map[s[left]]-- > 1){
                    count--;
                }
                left++;
            }
            ans = max(ans, r - left + 1); /*❹*/
        }
        return ans;
    }
};
```
❶ The property of the window. In this case, it is how many characters are repeated.  
❷ The condition to move right edge of the window.   
❸ The condition to move left edge of the window. In this case, if there is a character repeated, we need update left edge.  
❹ Update the result. The place we update result is different from leetcode 76. Why?  
