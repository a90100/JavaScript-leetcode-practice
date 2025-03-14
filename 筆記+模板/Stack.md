# Stack

使用 Stack 具有**用空間換時間**的概念，逆序處理也會想到 Stack。

> 逆序處理參考 [445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii)

還有一個特性是遞迴能完成的事情，透過 Stack 也能完成。

> Reason is that recursion relies on the call stack to manage function calls and handle the recursive process. On the other hand, a stack data structure can mimic the behavior of the call stack, allowing us to implement the same logic iteratively. This equivalence is based on the fact that both approaches follow the same depth-first traversal pattern

## Monotonic Stack

為 stack 內部數值保持遞增或遞減的 stack，如果新增的元素不符合 stack 內數值大小的規則，就 pop 出去，直到內部所有數值都保持遞增或遞減其一。

當需要往前或是往後尋找陣列中，下一個比自己大或比自己小的元素時可以思考使用。

### 時間複雜度

Monotonic Stack 的時間複雜度為 O(n)：

1. 每個元素最多只會被「壓入（push）」一次：在遍歷陣列的過程中，每個元素只會被放入堆疊一次。

2. 每個元素最多只會被「彈出（pop）」一次：當進入 while 迴圈時，會根據條件（如維持單調性）將堆疊中的元素彈出，但每個元素在彈出之後就不會再次被壓入。

總操作次數不會超過 2n：由於每個元素只能被壓入一次且彈出一次，因此即使 while 迴圈嵌套在 for 迴圈中，整個過程中堆疊的操作次數最多為 n 次壓入和 n 次彈出，合計 2n 次操作。

### Monotonic Increasing Stack

```javascript
function monotonicIncreasing(nums) {
  const stack = [];

  for (let i = 0; i < nums.length; i++) {
    while (stack.length && stack[stack.length - 1] > nums[i]) {
      stack.pop();
    }
    stack.push(nums[i]);
  }

  return stack;
}

const nums = [3, 1, 4, 1, 5, 9, 2, 6];
const result = monotonicIncreasing(nums); // [1, 1, 2, 6]
```

### Monotonic Decreasing Stack

```javascript
function monotonicDecreasing(nums) {
  const stack = [];

  for (let i = 0; i < nums.length; i++) {
    while (stack.length && stack[stack.length - 1] < nums[i]) {
      stack.pop();
    }
    stack.push(nums[i]);
  }

  return stack;
}

const nums = [9, 3, 1, 4, 1, 6, 2, 5];
const result = monotonicDecreasing(nums); // [9, 6, 5]
```

### 例題:

[739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures)
