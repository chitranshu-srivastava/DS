# Reverse pairs

### Problem Description

> Given an array of integers A, we call (i, j) an important reverse pair if i < j and A[i] > 2\*A[j].
> Return the number of important reverse pairs in the given array A.
> Return the number of important reverse pairs in the given array A.

### Problem Constraints

> 1 <= length of the array <= 105
>
> -2 _ 109 <= A[i] <= 2 _ 109

### Example Input and Output

> [Input] A = [1, 3, 2, 3, 1]
>
> [Output] 2
>
> [X] There are two pairs which are important reverse i.e (3, 1) and (3 1).
>
> [Input] A = [4, 1, 2]
>
> [Output] 1
>
> [X] There is only one pair i.e (4, 1).

## Solution

### Javascript

```
var reversePairs = function(nums) {
    return mergeSort(0, nums.length - 1, nums);
};
function merge(start, mid, end, A) {
  let a = [];
  let b = [];
  let one = start;
  let two = mid + 1;
  while (one <= mid) a.push(A[one++]);
  while (two <= end) b.push(A[two++]);

  one = two = 0;
  for (let id = start; id <= end; id++) {
    if (two >= b.length || a[one] < b[two]) A[id] = a[one++];
    else A[id] = b[two++];
  }
}

function mergeSort(start, end, A) {
  if (start == end) return 0;
  let mid = (start + end) >> 1;

  let ans = 0;
  ans += mergeSort(start, mid, A);
  ans += mergeSort(mid + 1, end, A);

  let j = mid;
  for (let i = start; i <= mid; i++) {
    while (j + 1 <= end && A[j + 1] * 2 < A[i]) j++;
    ans += j - (mid + 1) + 1;
  }
  merge(start, mid, end, A);
  return ans;
}

```
