# Set Matrix Zeros

There are two solutions to this problem. The one that I found easier to remember is the one where you use some space to keep track the indices that contain a zero. This solution, 
when using a set, at most will use O(N+M) space, where N is the number of rows, and M is the number of columns. My solution is below: 

## Storing Indicies solution
```java
class Solution {
    
    public void setRowZero(int[][] matrix, int targetRow) {
        for (int col = 0; col < matrix[0].length; col++) {
            matrix[targetRow][col] = 0; 
        }
    }
    
    public void setColZero(int[][] matrix, int targetCol) {
        for (int row = 0; row < matrix.length; row ++) {
            matrix[row][targetCol] = 0; 
        }
    }
    
    public void setZeroes(int[][] matrix) {
        HashSet<Integer> columns = new HashSet<Integer>(); 
        HashSet<Integer> rows = new HashSet<Integer>(); 
        
        
        for (int row = 0; row < matrix.length; row++) {
            for (int col = 0; col < matrix[0].length; col++) {
                if (matrix[row][col] == 0) {
                    rows.add(row); 
                    columns.add(col); 
                }
            }
        }
            
        for (Integer row: rows) {
            setRowZero(matrix, row); 
        }
    
        for (Integer col: columns) {
            setColZero(matrix, col); 
        }
    }
}
```

## Not using extra space. 
This soution requires a bit of a trick of using the first row, or the first column as the indicator of whether to set the curreent one equal to zero or not. 
