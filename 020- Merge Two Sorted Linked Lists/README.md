<h3> Problem </h3>
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

<pre>
    Input: list1 = [1,2,4], list2 = [1,3,4]
    Output: [1,1,2,3,4,4]
</pre>

<h3> Algorithm </h3>
<pre>
Step 1: initialize dummy new node
Step 2: compare values, if list1 value is greater than list2 value... add list2 element and go to next node
Step 3: repeat the same thing until list1 and list2 is not null
Step 4: if one list gets over then add the other list without comparison

**Note: 
Time Complexity = O(n + m)
Space Complexity = O(1)
**

</pre>

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode newListNode = new ListNode(0);
        ListNode head = newListNode;

        while(list1 !=null && list2 != null){
            if(list1.val < list2.val){
                head.next = list1;
                list1 = list1.next;
            }
            else{
                head.next = list2;
                list2 = list2.next;
            }
            head = head.next;
        }

        if(list1 !=null){
            head.next = list1;
        }
        else{
            head.next = list2;
        }
        return newListNode.next;
    }
}
``` </pre>