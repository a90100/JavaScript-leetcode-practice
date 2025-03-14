# Heap / Priority Queue

堆（Heap） 是一種特殊的樹形資料結構，只要滿足以下兩點的樹，就是堆：

1. Heap 是一個完全二元樹
2. Heap 中每一個節點的值都必須大於等於（或小於等於）其子樹中每個節點的值

第四個不是 Heap:

![](https://2xiao.github.io/leetcode-js/assets/2-7-1-uvdeiuE8.png)

之前寫的文章: [Day7-Heap 堆積](https://ithelp.ithome.com.tw/articles/10324806)

使用 [@datastructures-js/priority-queue](https://github.com/datastructures-js/priority-queue)

### 使用範例

1.

```javascript
// 初始化，使用 dis 的值當排序，MinPriorityQueue 也可以改成 MaxPriorityQueue
const minQueue = new MinPriorityQueue((point) => point.dis);

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
