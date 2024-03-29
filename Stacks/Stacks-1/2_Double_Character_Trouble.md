# Double Character Trouble

### Problem Description

> You are given a string A.
> An operation on the string is defined as follows:
> Remove the first occurrence of the same consecutive characters. eg for a string "abbcd", the first occurrence of same consecutive characters is "bb".
> Therefore the string after this operation will be "acd".
> Keep performing this operation on the string until there are no more occurrences of the same consecutive characters and return the final string.

### Problem Constraints

> 1 <= |A| <= 100000

### Example Input and Output

> [Input] A = abccbc
>
> [Output] "ac"

> [Input] A = ab
>
> [Output] "ab"

## Solution

### Javascript

```javascript
const solve = function (A) {
  let stack = [];
  for (let char of A) {
    if (stack[stack.length - 1] === char) {
      stack.pop();
    } else {
      stack.push(char);
    }
  }
  return stack.join("");
};
```

### Java

```java
public class Solution {
    public String solve(String A) {
        // we maintain a stack for the characters of the string
        Stack < Character > st = new Stack < Character > ();
        for (int i = 0; i < A.length(); i++) {
            // if the current character is equal to the top of the stack then they form 
            // a pair of consecutive similar characters therefore we pop from the stack,
            // else we push the charcter in the stack
            if (!st.empty() && st.peek() == A.charAt(i)) {
                st.pop();
            } else st.push(A.charAt(i));
        }
        StringBuilder sb = new StringBuilder();
        while (!st.empty()) {
            sb.append(st.peek());
            st.pop();
        }
        sb.reverse();
        return sb.toString();
    }
}
```
