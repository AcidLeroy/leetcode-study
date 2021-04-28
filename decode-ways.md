# Decode ways

This problem gave me quite a bit of trouble. Evening coming up with a recursive or backtracking solution evaded me for quite some time. 
With some help, I was able to come with a recursive solution. On leetcode, this gives you a *Time Limit Exceeded* problem. But for learning 
purposes, I think that it is ok. 

## Recursive solution 

```javascript
// Generates a mapping of all valid strings combinations
function generateValid() {
    let result = {}; 
    let num = 1; 
    for (let code = "A".charCodeAt(0); code <= 'Z'.charCodeAt(0); code++, num++){
        const key = ""+num; 
        result[key] = String.fromCharCode(code); 
    }
    
    return result; 
}


/**
 * @param {string} s
 * @return {number}
 */
var numDecodings = function(s) {
    const lut = generateValid(); 
    
    // This is the hard part. This check is to determine if we can add the current index and/or the next index. 
    // i.e. if we have "20", we are able to add both the 2 & and the 20. However, in the case of something like
    // "30" we are only able to add 3. The same goes for something lilke "03". 
    function check(s, ind) {
        let [b1, b2] = [false, false]; 
        if (ind < s.length) {
            if (lut[s[ind]]) b1 = true; 
            if (ind+1 < s.length) {
                if (lut[s[ind]+s[ind+1]]) b2 = true; 
            }
        }
        return [b1, b2]
    }
    
    function recursive(s, ind) {
        if(ind === s.length) return 1; 
        let count = 0; 
        const [b1, b2] = check(s, ind)
        if (b1) count += recursive(s, ind+1); 
        if (b2) count += recursive(s, ind+2); 
        return count; 
    }

    return recursive(s, 0);     
    
};

```

## DP solution coming soon
