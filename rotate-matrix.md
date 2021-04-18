# Rotate a matrix in place

This problem gave me quite a bit of trouble at first becuase it is quite easy to get the indicies all mixed up. 
The solution is rather simple, but is easy to mix up. Here are the steps that ultimately helped me solve the problem: 

1) Start on the outside and the work inward. In other words solve the outer layers of the matrix, then update some values to being working inwards. When you are done, update your pointers to move to the next section
2) When iterating over a layer, keep track of top, left, bottom and right pointers. Iterate from 0 - the length of that matrix
3) **Use pointers for bottom, top, left, and right**


Ultimately, here is my solution: 

```javascript
/*
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    
    // These pointers are key! 
    let [l, r] = [0, matrix.length - 1]
    
    while(l < r) {
        for (let i = 0; i < (r-l); i++){ // Notice the bounds here. I messed this up the first time. 
            // Since this is a square matrix, we can do it this way. 
            const [t, b] = [l, r]; 
            
            // console.log(`l = ${l} r = ${r}`)
            const topLeft = matrix[t][l + i];
            
            // Top left = bottom left
            matrix[t][l+i] = matrix[b - i][l]; 
            
            // Bottom left = bottom right 
            matrix[b - i][l] = matrix[b][r -i]; 
            
            // Bottom right = top right
            matrix[b][r - i] = matrix[t + i][r]; 
            
            // Top right = top left
            matrix[t + i][r] = topLeft; 
        }
        // After each "outer" calculation, update the left and right pointers to move inward. 
        l += 1; 
        r -= 1; 
    }
    
    
   
};
```
