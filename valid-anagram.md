# Valid Anagram

There are basically two methods for solving this problem 1) Sort then compare, 2) Use a hashmap to keep track of the number of letters in a string. 
The faster solution is to use the hashmap with the tradeoff of memory. Below, I use the hashmap method

## Hashmap Solution
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        // Need to determine an easy way to index into one string and delete
        // elements as needed
        // Hash map? uses extra space
        // Lookup/ remove more time complexity (search remove)
        
        // Hashmap way
        if (s.length() != t.length()) return false; 
        if (s.compareTo(t) == 0) return true; 
        
        HashMap<Character, Integer> m = new HashMap<Character,Integer>(); 
        for (int i = 0; i < s.length(); i++) {
            Character c = s.charAt(i); 
            if (m.containsKey(c)){
                Integer count = m.get(c) + 1; 
                m.put(c, count); 
            } else {
                m.put(c, 1); 
            }
        }
        
        for (int i = 0; i < t.length(); i++) {
            Character c = t.charAt(i); 
            if (m.containsKey(c)){
                Integer count = m.get(c) - 1;
                if (count == 0) m.remove(c); 
                else {
                    m.put(c, count); 
                }
            } else {
              return false;   
            }
        }
        return true; 
    }
}
```
