# Climbing Stairs problem (Dynamic Programming)

The key to this solution is to recognize a pattern. It's easy to rationalize the numbers from 0 to 4. 

For example: 
Number of stairs | Unique Combos
-----------------|--------------
0                | 0
1                | 1
2                | 2
3                | 3
4                | 5

As we can see from the table above, it appears that stairs[i] = stairs[i-1] + stairs[i-2]. This was not obvious to me at first, and one of the first solutions I wrote was 
an exhaustive search: i.e. I essentially I checked at each step if I held a value constant and then changed all the values. 
The wrong code looked like this: 

## ❌ WRONG
```java
class Solution {
    public int calcCombos(int stairs, int currSum) {
        if (currSum > stairs) return 0; 
        else if (currSum == stairs) return 1; 
        else {
            return calcCombos(stairs, currSum + 1) + calcCombos(stairs, currSum + 2); 
        }
    }
    public int climbStairs(int n) {
        return calcCombos(n, 0); 
    }
}
```
The above solution is correct, but it is not as an efficient as recognizing the pattern. This solution spans out in a binary way, so you get a time complexity of O(2^N), 
where N is the number of steps. 

## ✔️ RIGHT
In this solution, we exploit the pattern. As a result, the time complexity is O(N). 
```java
class Solution {
    public int climbStairs(int n) {
        int[] steps = new int[n+1]; 
        steps[0] = 0; 
        steps[1] = 1; 
        steps[2] = 2; 
        for (int i  = 3; i <= n; i++){
            steps[i] = steps[i-1] + steps[i-2]; 
        }
        
        return steps[n]; 
    }
}
```
