# Queue

JavaScript 本身並沒有內建這個資料結構，不過 LeetCode 有自動引入這兩個 Library，可以使用。

[@datastructures-js/queue](https://github.com/datastructures-js/queue/tree/v4.2.3)

[@datastructures-js/deque](https://github.com/datastructures-js/deque/tree/v1.0.4)

## Monotonic Queues

### Increasing Monotonic Queue

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

### Decreasing Monotonic Queue

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

## 雙端佇列 Deque

其發音為 deck，又稱 double-ended queue。 

https://weihanglo.tw/posts/2021/deque/
