<h3> Problem </h3>

You are given a string s consisting of the following characters: '(', ')', '{', '}', '[' and ']'.

The input string s is valid if and only if:

Every open bracket is closed by the same type of close bracket.
Open brackets are closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
Return true if s is a valid string, and false otherwise.

Example 1:

<pre>

&nbsp;   Input: s = "[]"

&nbsp;   Output: true

</pre>


Example 2:

<pre>

&nbsp;   Input: s = "[(])"

&nbsp;   Output: false

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Make a map where closing brackets have values of opening brackets and initialize a Stack where checking top most element and removing top most element is of cost O(1).
Step 2: check that if the current char is the closing bracket. if it is: then check if it's opening brackets is already there in the stack. If not then it means it's irregular parenthesis hence return false.
Step 2: if it's opening bracket is there, then remove that opening bracket as well.
Step 3: repeat the same step for other parenthesis.
Step 4: At last, check if the stack is empty or not, if empty then return true else false

**Note: 
Time Complexity = O(n)
Space Complexity = O(n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public boolean isValid(String s) {
        HashMap<Character, Character> charMap = new HashMap<>();
        charMap.put(')','(');
        charMap.put('}','{');
        charMap.put(']','[');
        Stack <Character> stack = new Stack<>();

        for(int i =0;i<s.length();i++){
            char c = s.charAt(i);
            if(charMap.containsKey(c)){
                if(!stack.isEmpty() && stack.peek()==charMap.get(c)){
                    stack.pop();
                }
                else{
                    return false;
                }
            }
            else{
                stack.push(c);
            }
        }
        return stack.isEmpty();
    }
}
``` </pre>