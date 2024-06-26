# Algorithm Template.md

## Array

### 建立 2D 陣列

```javascript
const twoDArr = new Array(rows).fill().map(() => new Array(cols).fill(0));
```

#### 例題:

- [2624. Snail Traversal](https://leetcode.com/problems/snail-traversal)

### Prefix Sum

[Prefix Sum（前綴和）概念](https://claire-chang.com/2023/05/04/prefix-sums%EF%BC%88%E5%89%8D%E7%B6%B4%E5%92%8C%EF%BC%89%E6%A6%82%E5%BF%B5/)

求**區段和**的題目，可以聯想到此演算法。

#### Prefix Sum LeetCode 題目列表

[Prefix Sum](https://leetcode.com/tag/prefix-sum/)

### 回溯法(BackTracking)

回溯法是一種找出問題所有解的演算法，常用遞迴的方式去窮舉各種結果的數值，一旦發現窮舉到和結果要求不符合的數值，就停止往下層窮舉下去，省去繼續往下探索的時間。

程式碼常會出現遞迴加上 push、pop 陣列元素的操作。

[五大基本算法之回溯算法 backtracking](https://houbb.github.io/2020/01/23/data-struct-learn-07-base-backtracking)

#### 例題:

- [39. Combination Sum](https://leetcode.com/problems/combination-sum)

## Queue

### Monotonic Queues

#### Increasing Monotonic Queue

陣列內只保留會逐漸遞增的元素，若接下來遍歷新元素，會從陣列後面開始將比當前遍歷元素大的都移除。

```javascript
function increasingMonotonicQueue(arr) {
  const q = [];

  for (let i = 0; i < arr.length; i++) {
    // If recently added element is greater than the current element
    while (q.length && q[q.length - 1] > arr[i]) {
      q.pop();
    }

    q.push(arr[i]);
  }

  return q;
}

const arr = [4, 2, 5, 1, 3, 6];
const q = increasingMonotonicQueue(arr);

console.log(q); // [1, 3, 6]
```

#### Decreasing Monotonic Queue

陣列內只保留會逐漸遞增的元素，若接下來遍歷新元素，會從陣列後面開始將比當前遍歷元素小的都移除。

```javascript
function decreasingMonotonicQueue(arr) {
  const q = [];

  for (let i = 0; i < arr.length; i++) {
    // If recently added element is smaller than current element
    while (q.length && q[q.length - 1] < arr[i]) {
      q.pop();
    }

    q.push(arr[i]);
  }
  return q;
}

const arr = [6, 4, 2, 5, 1, 3];
const q = decreasingMonotonicQueue(arr);

console.log(q); // [6, 5, 3]
```

## Stack

使用 Stack 具有**用空間換時間**的概念

### Monotonic Stack

為 stack 內部數值保持遞增或遞減的 stack，如果新增的元素不符合 stack 內數值大小的規則，就 pop 出去，直到內部所有數值都保持遞增或遞減其一。

當需要往前或是往後尋找陣列中，下一個比自己大或比自己小的元素時可以思考使用。

#### Monotonic Increasing Stack

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

#### Monotonic Decreasing Stack

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

#### 例題:

[739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures)

## Linked List

反轉鏈表 和 取鏈表的中間節點 是解 LeetCode 鏈表題很常用的操作，合併排序的鏈表有幾次也有用到

### 反轉鏈表

參考 LeetCode [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list) 這題

### 取鏈表的中間節點

參考 LeetCode [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list) 這題

### 合併排序的鏈表

參考 LeetCode [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists) 這題

### Doubly Linked List

[Implementation of Doubly Linked List in JavaScript](https://www.geeksforgeeks.org/implementation-of-doubly-linked-list-in-javascript/)

## 不算常用演算法

### Moore majority vote algorithm(摩爾投票演算法)

[如何理解摩尔投票算法？](https://www.zhihu.com/question/49973163)

優點: 空間複雜度低，適用大規模數據
缺點: 不適用沒出現主要元素的情況，找到主要元素還須進一步驗證是否是所求的值

使用題目:

- [169. Majority Element](https://leetcode.com/problems/majority-element/description/)
- [229. Majority Element II](https://leetcode.com/problems/majority-element-ii/description/)

### Manacher's Algorithm

以 O(n) 時間複雜度，查找一個字串的最長回文子字串的演算法。可參考 5. Longest Palindromic Substring 這題的筆記。

## 非演算法(一些語法)

### 函式 `Math.trunc()`

可以直接去掉小數點的數字

### Map.prototype.entries()、keys()、values()

```javascript
for (const [key, value] of hashMap.entries()) {
  // ...
}
```

## 待讀

https://medium.com/@derekfan/%E4%B9%9D%E7%AB%A0%E7%AE%97%E6%B3%95-template-binary-tree-iterative-pre-in-post-order-traversal-2af4625e086d
