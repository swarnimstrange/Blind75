<h3> Problem </h3>
Given the roots of two binary trees p and q, return true if the trees are equivalent, otherwise return false.

Two binary trees are considered equivalent if they share the exact same structure and the nodes have the same values.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/e78fc10c-4692-471f-5261-61e9be4f3a00/public">
    Input: p = [1,2,3], q = [1,2,3]
    Output: true
</pre>

Example 2:

<pre>

&nbsp;   Input: p = [4,7], q = [4,null,7]

&nbsp;   Output: false

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To find if the binary tree is same, we can both at the same time and if we find any difference at any place return false.
Step 2: there could be two type of difference in getting same binary tree, one can be left or right node of first tree is null but the second is not.
Step 3: second difference could be the difference in values. if both are not the issue then keep traversing until we reach the end of both tree and return true.

**Note: 
Time Complexity = O(n)
Space Complexity = O(n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        
        if(p == null && q == null){
            return true;
        }

        if((p != null && q == null) || (p == null && q != null)){
            return false;
        }

        if(p.val != q.val){
            return false;
        }

        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);

    }
}
``` </pre>