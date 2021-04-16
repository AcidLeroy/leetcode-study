# Pacific Atlantic Water flow

This problem stumped me for a bit because I was initially thinking about it wrong. My frist attempt at the problem was to follow this steps: 

1) For each row/col in the image
2) Do a depth first search at the cell. 
3) if a particular cell was marked as "able to go to pacific and atlantic" then it was part of the list


The problem for me, was I wanted to use an interative approach to solving the problem. The only way I could
mark a cell was either if it bordered either the atlantic or pacific ocean, or if an adjacent cell was already marked. 

A 1D example of why this is difficult is the following: 

Let's say you have an array of : `[1, 2, 3, 2, 1]`

The answer for this should be index "2" since it can flow both in the left direction and the right direction. 

The problem with looping over *every* element is that there are many instances where you cannot know if a cell flows
to either the left or the right. For example, let say I'm at index `3` in the above example. I can look at the cell
left and right, however, I have no idea whether either one can visist the atlanic or pacific, so I can't add anything to the stack. 
I won't be able to start traversing again until I get to the end of the array.

So here is the shortcut: iterate over the edges only, instead of all possible values. So in the 1D version, that looks like 
only start at the left, and then starting at the right. If you end up with indexes that have both left and right possibilities, 
then you know that that value is in the solution space. 

From there, I can apply the same logic to the 2D space. In this case, I just start with the solutions on each border. 

My solution is below: 

```javascript
function bfs(queue, heights){
   // bfs on pacific
    let visited = new Set();
    const numRows = heights.length; 
    const numCols = heights[0].length
    while(queue.length !== 0){
        const [row, col] = queue.shift(); 
        const val = heights[row][col]; 
        // console.log('row = ' + row + ' col = ' + col + ' val = ' + val); 

        if (!visited.has(JSON.stringify([row, col]))){
            visited.add(JSON.stringify([row, col])); 
            // check right
            if (col + 1 < numCols && heights[row][col+1] >= val ){
                queue.push([row, col + 1])
            }
            
            // Check below
            if (row + 1 < numRows && heights[row + 1][col] >= val){
                queue.push([row + 1, col ])
            }
            
            if (col - 1 >= 0 && heights[row][col-1] >= val ){
                // console.log('adding left = ', heights[row][col-1])
                queue.push([row, col - 1])
            }
            
            // Check above
            if (row - 1 >= 0 && heights[row - 1][col] >= val){
                // console.log('adding abov = ', heights[row-1][col])
                queue.push([row - 1, col ])
            }
        }
    }  
    
    return visited; 
}


/**
 * @param {number[][]} heights
 * @return {number[][]}
 */
var pacificAtlantic = function(heights) {
    
    
    const numRows = heights.length; 
    const numCols = heights[0].length; 
    
    let pacificQ = []; 
    let atlanticQ = []; 
    // Initialize pacific Ocean
    for (let row = 0; row < numRows; row++){
        for (let col = 0; col < numCols; col++){
            
            // top Row for pacific
            if (row === 0){
                pacificQ.push([row, col])
            }
            
            // left row for pacific
            if (row > 0 && col === 0){
                 pacificQ.push([row, col])
            }
            
            // right column for atlantic
            if (col === numCols - 1){
                atlanticQ.push([row, col]); 
            }
            
            // bottom row for atlantic
            
            if (row === numRows - 1 && col < numCols - 1){
                atlanticQ.push([row, col])
            }
        }
    }
    
    let pacificVisited = bfs(pacificQ, heights)
    let atlanticVisited = bfs(atlanticQ, heights); 
   
    
    // console.log("pacificVisited = ", pacificVisited); 
    // console.log("atlanticVisited = ", atlanticVisited); 
    
    let result = []; 
    let longer
    let shorter; 
    if ( pacificVisited.length > atlanticVisited.length){
        longer = pacificVisited; 
        shorter = atlanticVisited; 
    } else {
          longer = atlanticVisited; 
        shorter = pacificVisited; 
    }
    
    longer.forEach( p => {
        if (shorter.has(p)){
            result.push(p); 
        }
    })
    // console.log('result = ', result); 
    return result.map(x => JSON.parse(x)); 

   
};
```
