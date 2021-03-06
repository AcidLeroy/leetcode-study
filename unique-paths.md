# Unique Paths
This problem uses dynamic programming. I seem to continue to make the mistake of using an exhaustive, recursive approach to solve these types of problems. 
In others, I alwasy get the `Time Limit Exceeded` issue on leet code. Here is the result of my first appraoch

## ❌ Recursive solution with my attempt at memoization 

```java
class Solution {
    
    int m; 
    int n; 
    HashMap<Integer[], Integer> memo; 
    public int unique(int x, int y) {
        // System.out.println("x = " + x + " y = " + y); 
        // boundary conditions
        if (x >= this.m || y >= this.n) return 0; 
    
        if (x == this.m-1 && y == this.n-1){
            // reached a solution
            return 1; // Found a solution
        }
        Integer[] key = new Integer[]{x, y}; 
        
        if (this.memo.containsKey(key)){
            return this.memo.get(key); 
        }
        int right = unique(x + 1, y); 
        int down = unique(x, y + 1); 
        Integer ans =  right + down;    
        memo.put(key, ans); 
        return ans; 
    }
    
    public int uniquePaths(int m, int n) {
        this.m = m; 
        this.n = n; 
        this.memo = new HashMap<Integer[], Integer>(); 
        return unique(0, 0); 
```

My attempt at memoization doesn't help at all. 

## Actually using dynamic programming

In order to solve this problem, I think a good approach for me would be to start with 1x1, 2x2, and 3x3 to get the pattern

### 2x2
| <!-- -->    | <!-- -->    |
|-------------|-------------|
| 1         | 1         |
| 1 | 2|

### 3x3
| <!-- --> | <!-- --> | <!-- --> |
|------|------|-----|
| 1 | 1 | 1 |
| 1 | 2 | 3 | 
| 1 | 3 | 6 | 

### Anaylysis
From the above we start to see a trend. First of all, it wasn't obvious to me at first, but there is *exactly* one path on the top row and on the left-most column. This is 
true because if you think about it, there is really *is* only one path to those (if you got down, you'll never get back up, and if you got right, you'll never get left again). 
Additionally, we can see the the sum of the current cell is equal to the number in the cell above plus the cell to the left.

```java
```

