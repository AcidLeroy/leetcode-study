# Number of Islands

I have solved this problem a few times already, but on my last go around I didn't read the instructions close enough. I ended up thinking that *horizontal* connections
constituted a single lands mass. This is not the case. Additionally, I decided to solve the problem using a LinkedList Stack instead of through recursion, just to try something
different


## Solution using a linked list
```java
class Solution {
    
    public void zeroOut(char[][] grid, int i, int j){
        LinkedList<Integer[]> stack = new LinkedList<Integer[]>(); 
        stack.push(new Integer[]{i, j}); 
        int maxX = grid.length; 
        int maxY = grid[0].length; 
        
        while(stack.size() > 0){
            Integer[] curr = stack.pop(); 
            grid[curr[0]][curr[1]] = '0'; 
            // System.out.println("current = (" + curr[0] + ", " + curr[1] + ")"); 
            // System.out.println(grid[curr[0]][curr[1]] );
            Integer[][] list = new Integer[][]
            {{curr[0], curr[1]+1}, 
             {curr[0], curr[1]-1},
             {curr[0]+1,curr[1]},
             {curr[0]-1, curr[1]}
            }; 
            for(Integer[] p: list){
                if (p[0] >= 0 && p[0] < maxX && p[1] >=0 && p[1] < maxY){
                    if (grid[p[0]][p[1]] == '1'){
                        stack.push(p); 
                    }
                }
            }
                
            // System.out.println(); 
        }
        return; 
    }
    
    public void printGrid(char[][] grid) {
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                System.out.print(grid[i][j] + " "); 
            }
            System.out.println(); 
        }
    }
    public int numIslands(char[][] grid) {
        int islands = 0;
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1'){
                    islands++; 
                    // printGrid(grid); 

                    zeroOut(grid, i, j);
                    // System.out.println(); 
                }  
            }
        }
        
        return islands; 
    }
}
```
from the code above we see that need to iterate over each element inside the matrix, so the time complexity for outer loop is O(NxM) where N is the number of rows in the matrix and M
is the number of columns. The best case scenario would be that there are no 1s, therefore O(MxN) is the best case. For the case where everything is a 1, we would end up iterating through
the entire matrix twice, i.e. O(2xMxN) because we would set all the values to '0' on the first encounter with a '1'.


## Solution using recursion
```java
public class Solution {

private int n;
private int m;

public int numIslands(char[][] grid) {
    int count = 0;
    n = grid.length;
    if (n == 0) return 0;
    m = grid[0].length;
    for (int i = 0; i < n; i++){
        for (int j = 0; j < m; j++)
            if (grid[i][j] == '1') {
                DFSMarking(grid, i, j);
                ++count;
            }
    }    
    return count;
}

private void DFSMarking(char[][] grid, int i, int j) {
    if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] != '1') return;
    grid[i][j] = '0';
    DFSMarking(grid, i + 1, j);
    DFSMarking(grid, i - 1, j);
    DFSMarking(grid, i, j + 1);
    DFSMarking(grid, i, j - 1);
}
}
```

