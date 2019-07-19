## Description
>We have a list of points on the plane.  Find the K closest points to the origin (0, 0).
>
>(Here, the distance between two points on a plane is the Euclidean distance.)
>
>You may return the answer in any order.  The answer is guaranteed to be unique (except for the order that it is in.)
>
>Example 1:
Input: points = [[1,3],[-2,2]], K = 1
Output: [[-2,2]]
Explanation: 
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest K = 1 points from the origin, so the answer is just [[-2,2]].

>Example 2:
Input: points = [[3,3],[5,-1],[-2,4]], K = 2
Output: [[3,3],[-2,4]]
(The answer [[-2,4],[3,3]] would also be accepted.)
> 
>Note:
1 <= K <= points.length <= 10000
-10000 < points[i][0] < 10000
-10000 < points[i][1] < 10000

## Solution
This question is the TopK question. For this kind of question, there are two ways to do it.
- Use priority queue. Eg, top k largest, we can use size k min-heap. or can we use size N max-heap, which N is whole data size.
- Use quick selection. Leverage the quick sort approach. 

Here we are using second method. Time complexity average is O(n), worst is O(n^2), when pivot chosen is bad to reduce the data;

## Code
``` cpp
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int K) {
        int len = points.size(), l = 0, r = len - 1;
        kselection(points, l, r, K);
        return vector<vector<int>>(points.begin(), points.begin()+K);
    }
    void kselection(vector<vector<int>>& points, int l, int r, int k) {
        if(l >= r) return;                        /*❶*/
        vector<int>& pivot = points[r];           /*❷*/
        int i = l, j = l;
        while(j < r) {                            /*❸*/
            if(comparator(points[j], pivot) < 0) {
                swap(points[i++], points[j++]);
            } else {
                j++;
            }
        }
        swap(points[i], points[r]);               /*❹*/
        int num = i - l + 1;
        if(num > k) {
            kselection(points, l, i - 1, k);      /*❺*/
        } else if(num < k){
            kselection(points, i + 1, r, k - num);
        }
    }

    int comparator(vector<int>& lhs, vector<int>& rhs) {
        return lhs[0] * lhs[0] + lhs[1]*lhs[1] - rhs[0]* rhs[0] - rhs[1]*rhs[1];
    }
};
```
❶ Recursive base case.  
❷ Choose last element as pivot.  
❸ Three pointers approach for rainbow sort.  
❹ When while loop ends, i is the position of the first element which value is larger than pivot.  
❺ Decide which part we need to k select again.  

