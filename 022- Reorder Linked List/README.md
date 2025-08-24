<h3> Problem </h3>
You are given the head of a singly linked-list.

The positions of a linked list of length = 7 for example, can intially be represented as:

[0, 1, 2, 3, 4, 5, 6]

Reorder the nodes of the linked list to be in the following order:

[0, 6, 1, 5, 2, 4, 3]

Notice that in the general case for a list of length = n the nodes are reordered to be in the following order:

[0, n-1, 1, n-2, 2, n-3, ...]

You may not modify the values in the list's nodes, but instead you must reorder the nodes themselves.

<pre>

&nbsp;   Input: head = [2,4,6,8]

&nbsp;   Output: [2,8,4,6]

</pre>

Example 2:

<pre>

&nbsp;   Input: head = [2,4,6,8,10]

&nbsp;   Output: [2,10,4,8,6]

</pre>

<h3> Algorithm </h3>
<pre>
Step 1: traverse using two pointers using slow and fast. move slow one time and fast two times. then slow will reach at middle.
Step 2: then from middle node to the end, reverse the second half and make the last node as head of second linked list.
Step 3: make next of first node as temp, then traverse first node from first half and keep next as the right most element. keep next of right as temp2
Step 4: then repeat the third step until both of nodes are null.

**Note: 
Time Complexity = O(n)
Space Complexity = O(1)
**

</pre>

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public void reorderList(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast.next != null && fast.next.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        ListNode right = reverseLinkedList(slow);
        ListNode left = head;
        
        while(left != null && right!=null){
            ListNode leftNode = left.next;
            left.next = right;
            left = leftNode;
            ListNode rightNode = right.next;
            right.next = left;
            right = rightNode;
        }
    }

    public ListNode reverseLinkedList(ListNode head){
        ListNode curr = head;
        ListNode prev = null;

        while(curr != null){
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;

        }
        return prev;
    }
}
``` </pre>