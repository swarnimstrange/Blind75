<h3> Problem </h3>
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

<pre>
    <img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png">
    Input: head = [3,2,0,-4], pos = 1
    Output: true
    Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
</pre>

<h3> Algorithm </h3>
<pre>
Step 1: traverse using two pointers using slow and fast. move slow one time and fast two times.
Step 2: If it's a loop then fast will meet slow once and when it meets return true that it has cycle
Step 3: else if the linked list pointer gets null then it means it has no cycle, return false.

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
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) return true;
        }
        return false;
    }
}
``` </pre>