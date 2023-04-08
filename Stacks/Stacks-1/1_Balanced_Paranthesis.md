# Balanced Paranthesis

### Problem Description

> Given an expression string A, examine whether the pairs and the orders of “{“,”}”, ”(“,”)”, ”[“,”]” are correct in A.



### Problem Constraints

> 1 <= |A| <= 100

### Example Input and Output

> [Input] A = {([])}
>
> [Output] 1


> [Input] A = (){
>
> [Output] 0

> [Input] A = ()[]
>
> [Output] 0


## Solution

### Javascript

```javascript
const BalancedParanthesis = function (A) {
  let stack = [];
  let pairs = {
        '}':'{' ,
		']':'[' ,
		')':'(' ,
  }
  for(let char of A) {
    let delimeter = pairs[char];
    if(delimeter) {
        if(stack.pop() !== delimeter) {
            return 0;
        } 
    } else {
        stack.push(char);
    }
  }
  return stack.length == 0 ? 1 : 0;
};
```
### Java
```java
public class Solution {
    public int solve(String A) {
        HashMap < Character, Character > mp = new HashMap < Character, Character > ();
        Stack < Character > st = new Stack < Character > ();
        mp.put(')', '(');
        mp.put('}', '{');
        mp.put(']', '[');
        for (int i = 0; i < A.length(); i++) {
            char c = A.charAt(i);
            if (c == '(' || c == '[' || c == '{') {
                // push any opening bracket into the stack
                st.push(c);
            } else if (st.empty() || st.peek() != mp.get(c)) {
                // check if the last unpaired opening bracket is of the same type 
                // as the current closing bracket
                return 0;
            } else {
                st.pop();
            }
        }
        // checks if all the opening brackets are paired
        if (st.empty()) 
            return 1;
        return 0;
    }
}
```
