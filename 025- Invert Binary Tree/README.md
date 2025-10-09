<h3> Problem </h3>
You are given the root of a binary tree root. Invert the binary tree and return its root.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/ac124ee6-207f-41f6-3aaa-dfb35815f200/public">
    Input: root = [1,2,3,4,5,6,7]
    Output: [1,3,2,7,6,5,4]
</pre>

Example 2:

<pre>

&nbsp;   Input: root = [3,2,1]

&nbsp;   Output: [3,1,2]

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To invert the binary tree and return its root, first we have to invert the left and right one by one.
Step 2: Start with root node. interchange left and right node. 
Step 3: There's no need to check for their null values as if right is null and left node is not, then also it will interchange them and we will get the correct value.
Step 4: if the root left and right are interchanged. then traverse the root to it's left and right and perform the same action in recurtion.

**Note: 
Time Complexity = O(n)
Space Complexity = O(n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return null;
        }

        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;

        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
``` </pre>