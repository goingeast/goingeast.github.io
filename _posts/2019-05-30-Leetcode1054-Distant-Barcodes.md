---
categories: Leetcode
tag: A
---
### Description

> In a warehouse, there is a row of barcodes, where the i-th barcode is barcodes[i].
> 
> Rearrange the barcodes so that no two adjacent barcodes are equal. You may return any answer, and it is guaranteed an answer > exists.
> #### Example 1:
> Input: [1,1,1,2,2,2]  
> Output: [2,1,2,1,2,1]
> #### Example 2:
> Input: [1,1,1,1,2,2,3,3]  
> Output: [1,3,1,3,2,1,2,1]
> #### Note:
> 1 <= barcodes.length <= 10000  
> 1 <= barcodes[i] <= 10000  


### Solutions  

- Primitive idea, like greedy. As there is a guaranteed answer, we just get the most frequent element and fill in odd position first and then even position one by one.
- Heap method. Using template below. Basically, we are doing similar thing as the first greedy approach. 
  1. we put {element, frequency} to a max heap sorted by the frequency. 
  2. we keep popping K (here K is 2) elements from the heap and put to the result, then we decrease the frequency of the popped elements.
  3. goto step 1, push back to heap.  
  
### Similar Questions
Leetcode 358 Rearrange String  
Leetcode 621 Task Scheduler  

### Template

``` java
class Solution {
    public int[] rearrangeBarcodes(int[] barcodes) {
        if(barcodes == null || barcodes.length == 0)
            return new int[0];
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i: barcodes)
            map.put(i, map.getOrDefault(i, 0) + 1);
        PriorityQueue<Map.Entry<Integer, Integer>> pq = new PriorityQueue<Map.Entry<Integer, Integer>>(
		(a,b)->b.getValue()-a.getValue() == 0?a.getKey() - b.getKey(): b.getValue() - a.getValue());
        for(Map.Entry<Integer, Integer> entry:map.entrySet())
            pq.offer(entry);
        int[] res = new int[barcodes.length];
        int i = 0;
        while(!pq.isEmpty()) {
            int k = 2;
            List<Map.Entry> tempList = new ArrayList<Map.Entry>();
            while(k > 0 && !pq.isEmpty()) {
                Map.Entry<Integer, Integer> head = pq.poll();
                head.setValue(head.getValue() - 1);
                res[i++] = head.getKey();
                tempList.add(head);
                k--;
            }
            for(Map.Entry<Integer, Integer> e: tempList) {
                if(e.getValue() > 0) 
                    pq.add(e);
            }
            if(pq.isEmpty())
                break;
        }
        return res;
    }
}
    
```
