---
categories: Leetcode
---
## Description
>Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
>
>Example:
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
>
>Note:
If there is no such window in S that covers all characters in T, return the empty string "".
If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

## Solution
This is the classic sliding window question. All the sliding window question can use the template below. Pay an attention to all the steps, and try to understand it very well.
## Code
```cpp
class Solution {
public:
    string minWindow(string s, string t) {
       unordered_map<char, int> countMap;
       for(auto c: t) {                         /*❶*/
           countMap[c]++;
       }
       int left = 0;
       int count = countMap.size();
       int min = s.size();
       string res = "";
       for(int right = 0; right < s.size(); ++right) {
           if(countMap.count(s[right])) {       /*❷*/
               if(--countMap[s[right]] == 0) {
                   count --;
               }
           }
           while(count==0){
               if(right - left + 1 <= min) {    /*❸*/
                   min = right - left + 1; 
                   res = s.substr(left, min);
               }
               if(countMap.count(s[left])) {     /*❹*/
                   if( ++countMap[s[left]] > 0) {
                       count++;
                   }
               }
               left++;                           /*❹*/
           }
       }
       return res;
    }
};
```
❶ build a count map from the target  
❷ moving right side of a window, and update a certain state  
❸ update the result as the window is changed  
❹ update a certain condition as window is changed.  
❹ moving left side of the window, and in the while loop until it can not meet the condition.
