# Minimum Swaps 2

### Problem Description

> Given an array of integers A of size N that is a permutation of [0, 1, 2, ..., (N-1)]. It is allowed to swap any two elements (not necessarily consecutive).
> Find the minimum number of swaps required to sort the array in ascending order.

### Problem Constraints

> 1 <= N <= 100000
>
> 0 <= A[i] < N

### Example Input and Output

> [Input] A = [1, 2, 3, 4, 0]
>
> [Output] 4
>
> [X] If you swap (1, 2) -> (2, 3) -> (4, 0) -> (3, 0). You will get a sorted array. You cannot sort it with lesser swaps.
>
> [Input] A = [2, 0, 1, 3]
>
> [Output] 2
>
> [X] You cannot sort it with lesser than 2 swaps.

## Solution

### Javascript

```
const minSwaps = function(A) {
    let swaps = 0;
    for (let i = 0; i < A.length; i++) {
        while (A[i] !== i) {
            let temp = A[i];
            let tempII = A[A[i]];
            A[i] = tempII;
            A[temp] = temp;
            swaps++
        }
    }
    return swaps;
}

```
