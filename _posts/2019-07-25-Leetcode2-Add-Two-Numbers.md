#2019-07-25-Leetcode2-Add-Two-Numbers

---
categories: Leetcode
tags: F
---
## Description
>You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
>You may assume the two numbers do not contain any leading zero, except the number 0 itself.
>
>Example:
>Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) 
>Output: 7 -> 0 -> 8
>Explanation: 342 + 465 = 807.

## Solution
This is a linkedlist question. For linkedlist question, we can use a dummy head for clear solution. It is not hard question. Just remember how iterate the linkedlist.

## Code
```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry = 0;
        ListNode dummyHead(0);
        ListNode* iter = &dummyHead;   /*❶*/
        while(carry || l1 || l2) {     /*❷*/
            if(l1){
                carry += l1->val;
                l1 = l1->next;
            }
            if(l2) {
                carry += l2->val;
                l2 = l2->next;
            }
            iter->next = new ListNode(carry%10);
            iter = iter->next;
            carry /= 10;
        }
        return dummyHead.next;        /*❸*/
    }
};
```
❶ use a dummy head.  
❷	it is the template regarding to adding number with carry.  
❸ return dummy head's next.  
