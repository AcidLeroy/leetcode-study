# Maximum Depth of a Binary Tree
The easiest way to solve this problem is to use a recursive strategy. We need to keep track of what level we are currently at and if it is the maximum 

## Recursive strategy

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
