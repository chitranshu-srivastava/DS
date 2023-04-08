# Sort stack using another stack

### Problem Description

> Given a stack of integers A, sort it using another stack.
> Return the array of integers after sorting the stack using another stack.

### Problem Constraints

> 1 <= |A| <= 5000
> 0 <= A[i] <= 109

### Example Input and Output

> [Input] A = [5, 4, 3, 2, 1]
>
> [Output] [1, 2, 3, 4, 5]

> [Input] A = [5, 17, 100, 11]
>
> [Output] [5, 11, 17, 100]

## Solution

### Javascript

```javascript
const solve = function (A) {
  let temp = [];
  while (A.length > 0) {
    let tmp = A.pop();
    while (temp.length > 0 && temp[temp.length - 1] > tmp) {
      A.push(temp[temp.length - 1]);
      temp.pop();
    }
    temp.push(tmp);
  }
  return temp;
};
```

```javascript
class Stack {
  constructor() {
    this.items = [];
  }
  push(element) {
    this.items.push(element);
  }
  pop() {
    if (this.items.length == 0) return "Underflow";
    return this.items.pop();
  }
  top() {
    return this.items[this.items.length - 1];
  }
  empty() {
    return this.items.length == 0;
  }
  printStack() {
    var str = "";
    for (var i = 0; i < this.items.length; i++) str += this.items[i] + " ";
    return str;
  }
  clear() {
    this.items = [];
  }
}

function solve(A) {
  if (A.length <= 1) return A;
  let s1 = new Stack(),
    helper = new Stack();
  for (let i = 0; i < A.length; i++) {
    s1.push(A[i]);
  }
  while (!s1.empty()) {
    let temp = s1.top();
    s1.pop();
    // keep popping from helper till its top value is more than temp
    while (!helper.empty() && helper.top() > temp) {
      s1.push(helper.top());
      helper.pop();
    }
    helper.push(temp);
  }
  while (!helper.empty()) {
    s1.push(helper.top());
    helper.pop();
  }
  let arr = [];
  while (!s1.empty()) {
    arr.push(s1.top());
    s1.pop();
  }
  return arr;
}
```

### Java

```java
public class Solution {
  public int[] solve(int[] A) {

    if (A.length <= 1) return A;

    Stack < Integer > s1 = new Stack < Integer > ();
    Stack < Integer > helper = new Stack < Integer > ();
    for (int i = 0; i < A.length; i++) {
      s1.push(A[i]);
    }

    while (!s1.empty()) {
      int temp = s1.peek();
      s1.pop();
      // keep popping from helper till its peek value is more than temp
      while (!helper.empty() && helper.peek() > temp) {
        s1.push(helper.peek());
        helper.pop();
      }
      helper.push(temp);
    }
    while (!helper.empty()) {
      s1.push(helper.peek());
      helper.pop();
    }

    int ans[] = new int[A.length], i = 0;
    while (!s1.empty()) {
      ans[i] = s1.peek();;
      s1.pop();
      i++;
    }
    return ans;
  }
}
```
