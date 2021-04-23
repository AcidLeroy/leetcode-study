# Maximum width of a binary tree

This problem was tricky. Initially, I tried to solve it by filling in "null" nodes at levels where they needed to be, but this quickly became tricky and unmanageable. 
The trick to this problem is actually keeping track of the indices. Just like in a heap, we can use the formula to calculate what index of each node should be

I.e.

```
             0 
            /  \ 
           1    2  
         /  \   / \
        3   4  5   6
```

In other words, we have an array with the values: 0 1 2 3 4 5 6. To calculate the value at each index, we can use the formula `leftNode(idx) = idx*2 + 1` and `rightNode(idx) = idx*2+2`. As a result, we end up being able to label each node with this corresponding value.

The next aspect of this problem is to use BFS (I found this more intuitive). At each level, we iterate over each node to calcuate the index for the nodes below it. 
Once we have the index at each node, we can simply calculate the distance between them using the front and back of the queue with the corresponding index. 

## Solution using BFS
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 
              1             -- width = 1
             / \
            3   2           -- width = 2 
           / \
           
           
         1) Calculate width at each level, and keep track of it. 
         2) find the max of those.
 */

function getLeftIdx(idx) {
    return 2*idx + 1; 
}

function getRightIdx(idx) {
    return 2*idx + 2; 
}

/**
 * @param {TreeNode} root
 * @return {number}
 */
var widthOfBinaryTree = function(root) {
    if (!root) return 0; 
    
    const q = []; 
    
    let maxWidth = 1;
    
    // node and idx to queue
    q.push([root, 0]); 
    
    while(q.length > 0){
        
        const size = q.length; 
        const start  = q[0][1];
        const end = q[size-1][1]; 
        
        const width = end - start + 1;   
   
        maxWidth = Math.max(maxWidth, width); 
        
        for (let i = 0; i < size; i++) {  
            const p = q[0]; 
            const idx = p[1] - start; // This is extremely important for larger values. You end up overflowing your integers because of the massive size of the indexes as you iterate.
            const curr = q.shift();
            if (p[0].left) q.push([p[0].left, getLeftIdx(idx)]); 
            if (p[0].right) q.push([p[0].right, getRightIdx(idx)]); 
        }
                                   
    }
    
    return maxWidth; 
    
};
```
