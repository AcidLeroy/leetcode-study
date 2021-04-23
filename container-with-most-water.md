# Container with the most water

This problem has a really easy brute force solution, but the O(N) solution is hard to come up with. Initially, 
I thought that I could use two pointers going from left to right. In other words I thought there might be 
a way to to move only the left or right pointer based on what height/width was encountered next. This 
approach definitely does **not** work! Then I thought it might be possible to use a stack or something like that. 
Again, this approach led me no where because I couldn't intuitively come up with a way to keep track of the max
area using these methods. 

Ultimately, the solution does come down to two pointers, but where you start is key. 

1) You must start from either end of the array
2) Start working your way inwards
  a) If height at index left is less that height at index right, increment left pointer, otherwise decrement right pointer. 
  
  
## My solution is below: 
  
```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    let left = 0; 
    let right = height.length -1;
    let maxHeight = Number.MIN_SAFE_INTEGER; 
    
    while(left < right) {
        maxHeight = Math.max((right - left)*Math.min(height[left], height[right]), maxHeight); 
        height[left] < height[right] ? left++ : right--; 
    }
    return maxHeight; 
    
};
```
