# Evaluate Expression

### Problem Description

> An arithmetic expression is given by a string array A of size N. Evaluate the value of an arithmetic expression in Reverse Polish Notation.
> Valid operators are +, -, \*, /. Each string may be an integer or an operator.

### Problem Constraints

> 1 <= N <= 105

### Example Input and Output

> [Input] A = ["2", "1", "+", "3", "*"]
>
> [Output] 9

> [Input] A = ["4", "13", "5", "/", "+"]
>
> [Output] 6

## Solution

### Javascript

```javascript
const solve = function (A) {
  let stack = [];
  for (let i = 0; i < A.length; i++) {
    if (A[i] === "*" || A[i] === "+" || A[i] === "/" || A[i] === "-") {
      // pop the top two elements from the stack, perform the operation
      // and push that back into the stack
      let num2 = "(" + stack.pop() + ")";
      let num1 = "(" + stack.pop() + ")";
      stack.push(eval(num1 + A[i] + num2));
    } else {
      stack.push(A[i]);
    }
  }
  return parseInt(stack[0]);
};
```

### Java

```java
public class Solution {
    public int evalRPN(ArrayList < String > A) {
        Stack < Integer > values = new Stack < Integer > ();
        int first;
        int second;
        for (String str: A) {
            // on encountering an operator, pop the top two elements from the stack, 
            // perform the operation and push that back into the stack
            if (equal(str, "+")) {
                second = values.pop();
                first = values.pop();
                values.push(first + second);
            } else if (equal(str, "*")) {
                second = values.pop();
                first = values.pop();
                values.push(first * second);
            } else if (equal(str, "/")) {
                second = values.pop();
                first = values.pop();
                values.push(first / second);
            } else if (equal(str, "-")) {
                second = values.pop();
                first = values.pop();
                values.push(first - second);
            } else {
                first = Integer.parseInt(str);
                values.push(first);
            }
        }
        return values.peek();
    }
    public boolean equal(String str1, String str2) {
        return str1.equalsIgnoreCase(str2);
    }
}
```
