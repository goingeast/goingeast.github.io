## Description
>Given an array A of integers, return the length of the longest arithmetic subsequence in A.
>
>Recall that a subsequence of A is a list A[i_1], A[i_2], ..., A[i_k] with 0 <= i_1 < i_2 < ... < i_k <= A.length - 1, and that a >sequence B is arithmetic if B[i+1] - B[i] are all the same value (for 0 <= i < B.length - 1).
>
>Example 1:
Input: [3,6,9,12]
Output: 4
Explanation: 
The whole array is an arithmetic sequence with steps of length = 3.
>
>Example 2:
Input: [9,4,7,2,10]
Output: 3
Explanation: 
The longest arithmetic subsequence is [4,7,10].
>
>Example 3:
Input: [20,1,15,3,10,5,8]
Output: 4
Explanation: 
The longest arithmetic subsequence is [20,15,10,5].

## Solution
Use dynamic programming. This problem belongs to the second type of [DP](strstr.io) problem. Linear scan back the small result.   
$$dp[k][j]  = \max \limits_{j = 0 \dots i} dp[k][j]  \text { at index i} \tag{1}$$

$$dp[k][j]\text{ means the max length of sequence ended at index i with arithmetic difference k, j is in [0, i]} \tag{1}$$


## Code

```cpp
class Solution {
public:
    int longestArithSeqLength(vector<int>& A) {
        // diff vs (index vs length)
        const int MIN_LEN = 2;
        if(A.size() < MIN_LEN) return 1;
        unordered_map<int, unordered_map<int, int>> dp;
        int maxLen = DEFAULT_LEN;
        for(int i = 1; i < A.size(); ++i) {
            for(int j = 0; j < i; ++j) {
                int diff = A[j] - A[i];
                if(dp[diff].count(j)) {
                    dp[diff][i] = dp[diff][j] + 1;
                    maxLen = max(maxLen,dp[diff][i]);
                } else {
                    dp[diff][i] = MIN_LEN;
                }
            }
        }
        return maxLen;
    }
};
```
