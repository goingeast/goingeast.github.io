
## Description
>Return the root node of a binary search tree that matches the given preorder traversal.
>
>(Recall that a binary search tree is a binary tree where for every node, any descendant of node.left has a value < node.val, and any descendant of node.right has a value > node.val.  Also recall that a preorder traversal displays the value of the node first, then traverses node.left, then traverses node.right.
>
>Example 1:
Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
>
>Note: 
1 <= preorder.length <= 100
The values of preorder are distinct.

## Solution
- This can be solved by recursive approach described in this [thread](strstr.io). **NO(logN)**
- As it is BST, we can use the property of BST to make the algorithm faster. We compare pre order element to upperbound of the subtree, if the current value is bigger than the upperbound which means the current value should not be here. **O(N)**

## Code
```cpp
class Solution {
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        return bstFromPreorder(preorder, 0, preorder.size()-1);
    }
    
    TreeNode* bstFromPreorder(vector<int>& preorder, int left, int right){
        if(left > right){
            return NULL;
        }
        
        TreeNode* root = new TreeNode(preorder[left]);
        int upper = find(preorder, left+1, right, root->val);
        root->left = bstFromPreorder(preorder, left+1, upper-1);
        root->right = bstFromPreorder(preorder, upper, right);
        return root;
    }
    
    int find(vector<int>& preorder, int left, int right, int value){
        while(left <= right){
            if(preorder[left] < value){
                left++;
            }else{
                break;
            }
        }
        return left;
    }
};
```
``` cpp
class Solution {
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        int index = 0;
        int upperbound = INT_MAX;
        return bstFromPreorder(preorder, index, upperbound);
    }

    TreeNode* bstFromPreorder(vector<int>& preorder, int& index, int upperbound) {
        if(index == preorder.size() || preorder[index] > upperbound) {
            return nullptr;
        }
        TreeNode* root = new TreeNode(preorder[index++]);

        root->left = bstFromPreorder(preorder, index, root->val);
        root->right = bstFromPreorder(preorder, index, upperbound);

        return root;
    }

};
```
