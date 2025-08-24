<h3> Problem </h3>

You are given the beginning of a linked list head, and an integer n.

Remove the nth node from the end of the list and return the beginning of the list.

Example 1:

<pre>

&nbsp;   Input: head = [1,2,3,4], n = 2

&nbsp;   Output: [1,2,4]

</pre>


Example 2:

<pre>

&nbsp;   Input: head = [5], n = 1

&nbsp;   Output: []

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Find the count of all nodes through fast pointer, so that we can get it in n/2 of time. 
Step 2: once we have the count, subtract it with the k element so that we can get which element to remove. 
Step 2: once we have the element to remove...loop through the linked list, untill we find that element.
Step 3: once we have the element set previous of that element as next of the element.

**Note: 
Time Complexity = O(n)
Space Complexity = O(1)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode fast = head;
        int count = 0;

        while(fast.next != null && fast.next.next != null){
            fast = fast.next.next;
            count+=2;
        }
        if(fast.next != null){
            fast = fast.next;
            count +=1;
        }
        int needN = (count+1)-n;
        
        if (needN == 0) {
            return head.next;
        }
        count = 0;
        ListNode curr = head;
        ListNode prev = null;
        ListNode next = null;
        while(curr.next !=null && count<needN){
            prev = curr;
            curr = curr.next;
            count++;
        }
        if(curr.next != null ){
            next = curr.next;
        }
        prev.next = next;
        return head;
    }
}
``` </pre>