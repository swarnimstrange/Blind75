<h3> Problem </h3>
Implement an algorithm to serialize and deserialize a binary tree.

Serialization is the process of converting an in-memory structure into a sequence of bits so that it can be stored or sent across a network to be reconstructed later in another computer environment.

You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure. There is no additional restriction on how your serialization/deserialization algorithm should work.

Note: The input/output format in the examples is the same as how NeetCode serializes a binary tree. You do not necessarily need to follow this format.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/a9dfb17f-70e9-42a3-ba97-33cfd82f6100/public">
    Input: root = [1,2,3,null,null,4,5]
    Output: [1,2,3,null,null,4,5]
</pre>

Example 2:

<pre>
    Input: root = []
    Output: []
</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To solve this problem, we can do it using bfs queue method. So, to do that we have to run the tree in bfs sequence and keep appending the string and when we encounter null as node, append as N so that it can be later used to denote null in actual tree. 
Step 2: Now that we have the String, we have to run the tree in bfs again, setting the first element in String as root
Step 3: once we have the root, declare the index variable at 1, so that the root will not be picked up from string and we can start taking left and right values.
Step 4: for every left node node traversed, increase the index by 1, then do same for traversing right node. So, for every Node that gets polled, we get left and right value and the index goes 2+ so that we can get left and right values of next node.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
public class Codec {

    // Encodes a tree to a single string.
    StringBuilder treeString = new StringBuilder();
    public String serialize(TreeNode root) {
        if(root == null){
            return "N";
        }
        Queue< TreeNode > queue = new LinkedList<>();
        queue.add(root);
        treeString.append(root.val).append(",");;
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if(node.left != null){
                treeString.append(node.left.val).append(",");
                queue.add(node.left);
            }
            else{
                treeString.append("N,");
            }

            if(node.right != null){
                treeString.append(node.right.val).append(",");
                queue.add(node.right);
            }
            else{
                treeString.append("N,");
            }
        }
        System.out.println("treeString "+treeString);
        return treeString.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] array = data.split(",");
        if(array[0].equals("N")){
            return null;
        }
        Queue< TreeNode > queue = new LinkedList<>();
        TreeNode root = new TreeNode(Integer.parseInt(array[0]));
        queue.add(root);
        int index=1;
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if(!array[index].equals("N")){
                node.left = new TreeNode(Integer.parseInt(array[index]));
                queue.add(node.left);
            }
            index++;
            if(!array[index].equals("N")){
                node.right = new TreeNode(Integer.parseInt(array[index]));
                queue.add(node.right);
            }
            index++;
        }
        return root;
    }
}
``` </pre>