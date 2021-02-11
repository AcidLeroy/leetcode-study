# Maximum Depth of a Binary Tree
The easiest way to solve this problem is to use a recursive strategy. We need to keep track of what level we are currently at and if it is the maximum 

## Recursive strategy (depth first) 
```java
class Solution {
    public int depth(TreeNode root, int currentLevel){
        // If we reach a null node, return the current level 
        if (root == null) {
            return currentLevel; 
        }
        // Get the depth for the left and the right side (recursively calling this function)
        int left = this.depth(root.left, currentLevel+1); 
        int right = this.depth(root.right, currentLevel + 1); 
        
        // Compare which branch was the longest, either the left or othe right. 
        if (left > right) return left; 
        return right; 
    }
    public int maxDepth(TreeNode root) {
        // Call separate function with a starting depth of 0; 
        return depth(root, 0);  
    }
}
```

## Stack strategy (depth first, just for fun)
In this example, I demonsrate how to solve the problem using a stack instead of the recursive strategy: 

```java
class Solution {

    boolean isLeaf(TreeNode node) {
        return node.right == null && node.left == null; 
    }
    public int maxDepth(TreeNode root) {
        if (root == null) return 0; 
        Stack<TreeNode> st=  new Stack<TreeNode>(); 
        st.addElement(root);
        
        int max = 0; 
        // The reason I use a hashmap here is because I need to keep track of the current level I am at. 
        HashMap<TreeNode, Integer>  m = new HashMap<TreeNode, Integer>(); 
        
        // Initialize the stack, with the level value. 
        m.put(root, 1); 
        
        while(!st.empty()){
            // Pop a node off of the stack
            TreeNode n = st.pop();
            // Get what level the curren tnode is at. 
            Integer currentLevel = m.get(n); 
            
            // If we are at a leaf node, i.e. we don't have any children nodes, then we either 
            // update the max or not, then we pop the next thing off the stack. 
            if (isLeaf(n)){
                // Check max and update
                if (currentLevel > max) max = currentLevel; 
                continue;
            }  
            if (n.right != null) {
                m.put(n.right, currentLevel+1); 
                st.addElement(n.right);
            }
            if (n.left != null) {
                m.put(n.left, currentLevel + 1); 
                st.addElement(n.left);
            }
        }
        return max; 
    }
}
```
