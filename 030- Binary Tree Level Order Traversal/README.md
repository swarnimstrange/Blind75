<h3> Problem </h3>
Given a binary tree root, return the level order traversal of it as a nested list, where each sublist contains the values of nodes at a particular level in the tree, from left to right.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/a4639809-0754-4eda-221f-a4cd58bd9c00/public">
    Input: root = [1,2,3,4,5,6,7]
    Output: [[1],[2,3],[4,5,6,7]]
</pre>

Example 2:

<pre>

&nbsp;   Input: root = [1]

&nbsp;   Output: [[1]]

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  first thing to keep in mind is that, when we want to know the depth, we have to add the depth in traversal function call itself.
Step 2: that will save us from doing multiple increments based on traversal calls and will only increment if it reaches a new level.
Step 3: when we reach a new level add a new Array in list, then append based on the depth.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    List< List< Integer >> lord = new ArrayList<>();
    int maxCount = 0;
    public List< List< Integer >> levelOrder(TreeNode root) {
        LODT(root, 0);
        return lord;
    }

    public TreeNode LODT(TreeNode root, int count){
        if(root == null){
            return null;
        }

        if(lord.size() == count){
            lord.add(new ArrayList<>());
        }

        lord.get(count).add(root.val);
        LODT(root.left, count+1);
        LODT(root.right, count+1);
        return root;
    }

}
``` </pre>