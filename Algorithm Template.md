# Algorithm Template.md

## Array

### 建立 2D 陣列

```javascript
const twoDArr = new Array(rows).fill().map(() => new Array(cols).fill(0));
```

[How can I create a two-dimensional array in JavaScript?](https://sentry.io/answers/how-can-i-create-a-two-dimensional-array-in-javascript/)

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

## HashMap、HashSet

### 做 mapping 的內建函式有以下這些

都可以用 forEach 做 mapping。

#### 例題:

[347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)

#### Map.prototype.entries()、keys()、values()

```javascript
for (const [key, value] of hashMap.entries()) {
  // ...
}
```

### 將取到的 keys、values 轉成陣列

```javascript
const map = new Map();

map.set(1, '1');
map.set(2, '2');

console.log(Array.from(map.values()));

const mySet = new Set([1, 1, 2, 3, 4, 4, 5, 6, 5]);
let myArr = Array.from(mySet); // [1, 2, 3, 4, 5, 6]
```

### 更新 HashMap

如果 value 是陣列，用這種寫法而不是 Spread Operator

```javascript
// O(1)
const values = hashMap.get(key) || [];
values.push(newObj);
hashMap.set(key, values);

// O(n)
hashMap.set(key, hashMap.get(key) ? [...hashMap.get(key), newObj] : [newObj]);
```

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

## Binary Tree

> Tree is special form of graph.

### BFS(Breadth-First Search)

```javascript
const BFS = (root) => {
  const queue = [root];
  const res = [];

  while (queue[0]) {
    const currQueueLength = queue.length;

    for (let i = 0; i < currQueueLength; i++) {
      let cur = queue.shift();
      res.push(cur);

      if (cur.left) queue.push(cur.left);
      if (cur.right) queue.push(cur.right);
    }
  }

  return res;
};
```

#### 例題:

[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)

### Preorder Traversal(前序遍歷)

先拜訪父節點再拜訪左右子節點。

```javascript
function preorderTraversal(node) {
  // Base case
  if (node === null) return;

  // Visit the current node
  console.log(node.data + ' ');

  // Recur on the left subtree
  preorderTraversal(node.left);

  // Recur on the right subtree
  preorderTraversal(node.right);
}
```

[Preorder Traversal of Binary Tree](https://www.geeksforgeeks.org/preorder-traversal-of-binary-tree)

#### 例題:

[114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)

### Inorder Traversal(中序遍歷)

會先拜訪左子節點，再拜訪父節點，最後拜訪右子節點。

> 遍歷 Binary Search Tree，會得到由小到大的節點

```javascript
function printInorder(node) {
  if (node === null) return;

  // First recur on left subtree
  printInorder(node.left);

  // Now deal with the node
  console.log(node.data);

  // Then recur on right subtree
  printInorder(node.right);
}
```

[Inorder Traversal of Binary Tree](https://www.geeksforgeeks.org/inorder-traversal-of-binary-tree)

#### 例題:

[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst)

[173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator)

### Postorder traversal(後序遍歷)

先拜訪左右子節點，最後拜訪父節點。

```javascript
function postorderTraversal(node) {
  // Base case
  if (node === null) return;

  // Recur on the left subtree
  postorderTraversal(node.left);

  // Recur on the right subtree
  postorderTraversal(node.right);

  // Visit the current node
  console.log(node.data);
}
```

[Postorder Traversal of Binary Tree](https://www.geeksforgeeks.org/postorder-traversal-of-binary-tree)

### Binary Search Tree

1. 若任意節點的左子樹不空，則左子樹上所有節點的值均小於它的根節點的值
2. 若任意節點的右子樹不空，則右子樹上所有節點的值均大於它的根節點的值
3. 任意節點的左、右子樹也分別為二元搜尋樹
4. 二元搜尋樹相比於其他資料結構的優勢在於尋找、插入的時間複雜度較低，為 `O(log n)`。

#### 例題:

[450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst)

> 思考: 刪除節點後的更新情況有哪幾種?

### Complete Binary Tree

各層節點全滿，除了最後一層，最後一層節點全部靠左。

#### 例題:

[222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes)

## Binary Search

二分的本質是「二段性」而非「單調性」。

[二分法的二段性、两套模板 和 答案判定](https://writings.sh/post/binary-search)

```javascript
var search = function (nums, target) {
  let l = 0;
  let r = nums.length - 1;

  while (l <= r) {
    const mid = Math.floor((l + r) / 2);
    if (nums[mid] === target) return mid;
    if (nums[mid] > target) {
      r = mid - 1;
    } else {
      l = mid + 1;
    }
  }
  return -1;
};
```

#### 例題:

[162. Find Peak Element](https://leetcode.com/problems/find-peak-element)

## Graph

### DFS & BFS

#### 例題:

[200. Number of Islands](https://leetcode.com/problems/number-of-islands)

> DFS、BFS 都能解

[79. Word Search](https://leetcode.com/problems/word-search)

> DFS

### Topological sorting 拓撲排序

拓撲排序是針對特定種類圖的演算法: Directed acyclic graph (DAG)，有向無環圖。撰寫此演算法時常會宣告有關圖的 indegree(入度)。

> 有向無環圖為**邊有方向，圖內無環**的圖。

應用範例: 選課系統的先修課，要先修完某些課才能修指定課程

#### 例題:

[207. Course Schedule](https://leetcode.com/problems/course-schedule)

[310. Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees)

### Union-Find 併查集

最重要的 find、union 函式:

```javascript
const parents = [];

const find = (x) => {
  if (parents[x] !== x) {
    parents[x] = find(parents[x]);
  }

  return parents[x];
};

const union = (x, y) => {
  parents[find(x)] = find(y);
};
```

更完整:

[Union-Find 算法详解](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/UnionFind%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3.md)

#### 例題:

[547. Number of Provinces](https://leetcode.com/problems/number-of-provinces)

### Bellman Ford algorithm(貝爾曼-福特演算法)

假設一個圖有 v 個點，會進行 v - 1 次的迴圈計算，每次計算的最短路徑值會漸漸地被更加準確的值替代，直至得到最佳解。

> 不能計算負權環圖，因為負權環可以無限制的降低總花費

[Bellman Ford Algorithm | Shortest path & Negative cycles | Graph Theory](https://youtu.be/lyw4FaxrwHg)

[BellmanFord 算法详解(注意根据标好的顺序观看)](https://youtube.com/playlist?list=PLf4URHiWMndm3NfqFdebywKPZ6Uktn9Sw&si=o4WNk2xzfRX2SBRE)

> 3. Bellmanford 算法 3--动态规划解决 為主

#### 例題:

[787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops)

## Heap / Priority Queue

使用 [@datastructures-js/priority-queue](https://github.com/datastructures-js/priority-queue/blob/v5/README.md)

#### 使用範例

1.

```javascript
// 初始化，使用 dis 的值當排序，MinPriorityQueue 也可以改成 MaxPriorityQueue
const minQueue = new MinPriorityQueue({ priority: (point) => point.dis });

// 加入元素到 queue
minQueue.enqueue({ dis /*其他...*/ });

// 取出元素
minQueue.dequeue();

// 取出元素格式
// {
//   priority: 根據 dis 值而定,
//   element: { dis: 根據 dis 值而定, 其他... }
// }
```

2.

```javascript
const minQueue = new MinPriorityQueue();

// 加入元素到 queue
minQueue.enqueue(num);

// 取出元素
minQueue.dequeue();

// 取出元素格式
// {
//   priority: num,
//   element: num
// }
```

3.

```javascript
// 例題: 692. Top K Frequent Words
// 若要考慮到兩個以上的 priority 可以這樣寫:

const maxHeap = new MaxPriorityQueue({
  compare: (e1, e2) => {
    if (e1.freq > e2.freq) return -1; // do not swap
    if (e1.freq < e2.freq) return 1; // swap
    return e1.word < e2.word ? -1 : 1;
  },
});

// 加入元素到 queue
maxHeap.enqueue({ freq: value, word: key });

// 取出元素
maxHeap.dequeue();

// 取出元素格式 (直接取得存入的物件本身)
// { freq: 2, word: 'i' }
```

4.

```javascript
// 其他種寫法
const patientsQueue = new MinPriorityQueue();

patientsQueue
  .enqueue('patient y', 1) // highest priority
  .enqueue('patient z', 3)
  .enqueue('patient w', 4) // lowest priority
  .enqueue('patient x', 2);

console.log(patientsQueue.toArray());
// [
//   { priority: 1, element: 'patient y' },
//   { priority: 2, element: 'patient x' },
//   { priority: 3, element: 'patient z' },
//   { priority: 4, element: 'patient w' }
// ]
```

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

#### 例題:

[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring)

### Floyd Cycle Detection Algorithm(Floyd 判圈算法)

Floyd 判圈算法，又稱龜兔賽跑算法(Tortoise and Hare Algorithm)，是一個可以在有限狀態機、迭代函數或者鍊表上判斷是否存在環，求出該環的起點與長度的算法。

#### 例題:

[287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number)

### Morris traversal 莫里斯遍歷

[Algorithm 演算法 - 樹遍歷系列 Morris traversal 莫里斯遍歷](https://blog.taiwolskit.com/algorithm-morris-traversal)

### Segment Tree 線段樹

#### 例題:

[729. My Calendar I](https://leetcode.com/problems/my-calendar-i)

#### 例題:

[114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)

## 非演算法(一些語法)

### 函式 `Math.trunc()`

可以直接去掉小數點的數字。

### String.prototype.repeat()

重複字串指定的次數。

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat

### 取亂數

> 生成 0 ~ x 間的亂數

```javascript
function getRandom(x) {
  return Math.floor(Math.random() * x);
}
```

### [Bitwise AND (&)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_AND)

可以計算兩個數字其二進位數的每個位元是否都為一然後輸出

```javascript
const a = 5; // 00000000000000000000000000000101
const b = 3; // 00000000000000000000000000000011

console.log(a & b); // 00000000000000000000000000000001
```

### [Bitwise XOR (^)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_XOR)

兩個數字轉成二進位後，兩個數相同位元只要不是都是 1 或 0 就輸出 1

> 特性 兩個數做 ^ 會變成 0，可練習 [136. Single Number](https://leetcode.com/problems/single-number)

```javascript
const a = 5; // 00000000000000000000000000000101
const b = 3; // 00000000000000000000000000000011

console.log(a ^ b); // 00000000000000000000000000000110
// Expected output: 6
```

### (左、右)位移位運算子、無符號右位移運算子

- [Left shift (<<)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Left_shift)
- [Right shift (>>)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Right_shift)
- [Unsigned right shift (>>>)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Unsigned_right_shift)

```javascript
const a = 5; // 00000000000000000000000000000101
const b = 2; // 00000000000000000000000000000010

console.log(a << b); // 00000000000000000000000000010100
// Expected output: 20
//-----------------------------------------------------------
const a = 5; //  00000000000000000000000000000101
const b = 2; //  00000000000000000000000000000010
const c = -5; //  11111111111111111111111111111011

console.log(a >> b); //  00000000000000000000000000000001
// Expected output: 1

console.log(c >> b); //  11111111111111111111111111111110
// Expected output: -2
//-----------------------------------------------------------
const a = 5; //  00000000000000000000000000000101
const b = 2; //  00000000000000000000000000000010
const c = -5; //  11111111111111111111111111111011

console.log(a >>> b); //  00000000000000000000000000000001
// Expected output: 1

console.log(c >>> b); //  00111111111111111111111111111110，差異在整個數字右移後，前面補上 b 個 0
// Expected output: 1073741822
```

## 其餘補充

### 貪婪演算法(greedy algorithm)

[貪婪演算法](https://zh.wikipedia.org/zh-tw/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95)

### if / else 以前沒注意過的特性

參考 6. Zigzag Conversion 的筆記

### Modulo 10^9+7 (1000000007)

參考資料: https://www.geeksforgeeks.org/modulo-1097-1000000007/

以下 CHAT GPT 解釋:

Modulo 10^9 + 7 (1000000007) 是一個非常常見的模數，特別是在競賽編程和算法設計中。

這個數字有幾個重要的特性：

1. 大質數：1000000007 是一個質數，因此當進行模運算時，它保證了乘法、加法等操作的結果是唯一且可逆的。例如，模數為質數時，乘法的逆元一定存在（可以使用擴展歐幾里得算法或快速冪算法來計算乘法逆元）。
2. 防止數字溢出：在處理涉及大數的問題時，數值運算結果可能會超出計算機中整數的範圍（例如 C++ 中 int 類型的上限是約 2^31-1）。模 10^9 + 7 可以使結果保持在一個相對較小的範圍內，避免溢出。
3. 效率高：1000000007 足夠大，使得在許多應用中它可以防止碰撞（例如哈希函數），同時也足夠小，使得計算效率高（如取模、乘法逆等）。

常見應用：

1. 計算大數問題：例如在計算大階乘、指數運算等時，由於數值會迅速增大，模數可以保持結果在可控範圍內。
2. 動態規劃與組合數學：特別是在求解涉及排列、組合、二項式係數等問題時。

### 雙端佇列 Deque

https://weihanglo.tw/posts/2021/deque/

### 打週賽

1. input、測資不大時，有時可以暴力解題目，比較快完成而且出 bug 機率更少，比完再來優化，不過面試時又是另一回事
