<h3> Problem </h3>

You are given an array of k linked lists lists, where each list is sorted in ascending order.

Return the sorted linked list that is the result of merging all of the individual linked lists.

Example 1:

<pre>

&nbsp;   Input: lists = [[1,2,4],[1,3,5],[3,6]]

&nbsp;   Output: [1,1,2,3,3,4,5,6]

</pre>


Example 2:

<pre>

&nbsp;   Input: lists = []

&nbsp;   Output: []

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To merge k different linked list in one, we can go ahead with iterative approach
Step 2: for example if we have 3 different lists, then we can merge the first two, and set it as sorted in the second linked list.
Step 3: then we can use the sorted list of the two list to comapre and sort it with the remaining list.
Step 4: once reached the end, return the last linked list which is the sorted combination of all.

**Note: 
Time Complexity = O(n*k)
Space Complexity = O(1)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {

        if(lists.length == 0){
            return null;
        }

        for(int i=1; i < lists.length; i++){
            lists[i] = mergeLinkedList(lists[i], lists[i-1]);
        }
        return lists[lists.length - 1];
    }

    public ListNode mergeLinkedList(ListNode L1, ListNode L2){
        ListNode mergedLinkedList = new ListNode();
        ListNode dummy = mergedLinkedList;

        while(L1 != null && L2 != null){
            if(L1.val > L2.val){
                dummy.next = L2;
                L2 = L2.next;
            }
            else{
                dummy.next = L1;
                L1 = L1.next;
            }
            dummy = dummy.next;
        }
        if(L1 == null){
            dummy.next = L2;
        }
        else{
            dummy.next = L1;
        }
        return mergedLinkedList.next;
    }
}
``` </pre>