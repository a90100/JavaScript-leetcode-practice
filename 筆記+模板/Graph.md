# Graph

## 透過 adjacency list 建圖的模板

```javascript
const graph = new Map();

for (const [e, v] of edges) {
  if (!graph.has(e)) graph.set(e, []);
  graph.get(e).push(v);
  if (!graph.has(v)) graph.set(v, []);
  graph.get(v).push(e);
}
```

## DFS & BFS

DFS 有「使用全域變數維護」和「接收返回值處理」兩種形式。

### 例題:

[1730. Shortest Path to Get Food](https://leetcode.com/problems/shortest-path-to-get-food)

> BFS

[200. Number of Islands](https://leetcode.com/problems/number-of-islands)

> DFS、BFS 都能解

[79. Word Search](https://leetcode.com/problems/word-search)

> DFS

Tip: DFS 時多傳入一個參數 prev 代表當前節點的父節點。

[261. Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree)

## 0-1 BFS

邊權重只有 0 or 1 時，可以使用來找最短路徑。

和一般 BFS 的差別是，維護的 queue 是 雙端佇列(double-ended queue)，遇到 0 權重邊加入 queue 首，遇到 1 權重邊加入 queue 尾，

整個 queue 看起來就像 Increasing Monotonic Queue。

### 例題:

[2290. Minimum Obstacle Removal to Reach Corner](https://leetcode.com/problems/minimum-obstacle-removal-to-reach-corner)

## Topological sorting 拓撲排序

拓撲排序是針對特定種類圖的演算法: Directed acyclic graph (DAG)，有向無環圖，一種對有向無環圖的所有節點的一種排序，使得對每一條有向邊 (u, v)，在排序中節點 u 在節點 v 之前。

> 有向無環圖為**邊有方向，圖內無環**的圖。

> 在图论中，一个有向无环图必然存在至少一个拓扑序与之对应，反之亦然。

> 入度：有多少条边直接指向该节点；出度：由该节点指出边的有多少条。

應用範例: 選課系統的先修課，要先修完某些課才能修指定課程

### 優質介紹文

[【宫水三叶の相信科学系列】详解何为拓扑排序，以及求拓扑排序方法的正确性证明](https://leetcode.cn/problems/find-eventual-safe-states/solutions/916548/gong-shui-san-xie-noxiang-xin-ke-xue-xi-isy6u/)

### 模板

```javascript
var minimumSemesters = function (n, relations) {
  const graph = new Map();
  const indegrees = new Array(n + 1).fill(0);
  const queue = [];
  const visited = new Set();

  for (const [e, v] of relations) {
    graph.has(e) ? graph.get(e).push(v) : graph.set(e, [v]);
    indegrees[v]++;
  }

  for (let i = 1; i < indegrees.length; i++) {
    if (indegrees[i] === 0) queue.push(i);
  }

  while (queue.length) {
    let len = queue.length;

    for (let i = 0; i < len; i++) {
      const node = queue.shift();
      if (visited.has(node)) continue;
      visited.add(node);

      const neighbors = graph.get(node) ?? [];
      for (let neighbor of neighbors) {
        if (--indegrees[neighbor] === 0) queue.push(neighbor);
      }
    }
  }
};
```

### 例題:

[207. Course Schedule](https://leetcode.com/problems/course-schedule)

[310. Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees)

## Union-Find 並查集，Disjoint Set Union-find algorithm (DSU)

最重要的 find、union 函式:

```javascript
// 陣列
const parents = [];

// 設有 n 個點
for (let i = 0; i < n; i++) {
  parents.push(i);
}

const find = (x) => {
  if (parents[x] !== x) {
    parents[x] = find(parents[x]);
  }

  return parents[x];
};

const union = (x, y) => {
  parents[find(x)] = find(y);
};

// 物件
const uf = {};

function find(x) {
  if (uf[x] != x) uf[x] = find(uf[x]);
  return uf[x];
}

function union(x, y) {
  const rootX = find(x);
  const rootY = find(y);

  if (rootX === rootY) return;
  uf[rootX] = rootY;
}
```

在一開始初始化 parents 時，需要的時間複雜度為 O(n)，其中 n 為元素數量。

`Find()` 需要的時間複雜度為 O(α(n))，其中 α 是 inverse Ackermann function，它會成長非常地慢，所以可以將它視為常數時間。所以，O(α(n)) ≈ O(1)。因此，`Find()` 的時間複雜度為 O(1)。

`Union()` 使用到 `Find()`，所以它的時間複雜度是 O(1)。

Union Find data structure 內部需要一個 parents。所以，它的空間複雜度為 O(n)。

更完整:

[Union-Find 算法详解](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/UnionFind%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3.md)

[UnionFind 并查集算法详解](https://zhuanlan.zhihu.com/p/98406740)

### 例題:

[547. Number of Provinces](https://leetcode.com/problems/number-of-provinces)

[684. Redundant Connection](https://leetcode.com/problems/redundant-connection)

## Dijkstra's Algorithm(戴克斯特拉演算法)

最短路徑演算法，BFS + Heap

[Day5-Dijkstra's Algorithm(戴克斯特拉演算法)](https://ithelp.ithome.com.tw/articles/10323129)

### 例題:

[743. Network Delay Time](https://leetcode.com/problems/network-delay-time)

[3341. Find Minimum Time to Reach Last Room I](https://leetcode.com/problems/find-minimum-time-to-reach-last-room-i)

## Bellman Ford algorithm(貝爾曼-福特演算法)

假設一個圖有 v 個點，會進行 v - 1 次的迴圈計算，每次計算的最短路徑值會漸漸地被更加準確的值替代，直至得到最佳解。

Bellman-Ford 算法能處理帶有負權邊的圖，因此廣泛應用於解決具有負權邊的最短路徑問題。

[Bellman Ford Algorithm | Shortest path & Negative cycles | Graph Theory](https://youtu.be/lyw4FaxrwHg)

[BellmanFord 算法详解(注意根据标好的顺序观看)](https://youtube.com/playlist?list=PLf4URHiWMndm3NfqFdebywKPZ6Uktn9Sw&si=o4WNk2xzfRX2SBRE)

> 3. Bellmanford 算法 3--动态规划解决 為主

### 例題:

[787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops)

## 二分圖(Bipartite graph)

若無向圖 G=(V,E) 的頂點集 V 可以分割為兩個互不相交的子集，且圖中每條邊的兩個頂點分別屬於不同的子集，則稱圖 G 為一個二分圖。

這張圖可以很好的說明此特性：把節點上色，一個點相連的所有節點是屬於另一個子集的節點。

https://gmlwjd9405.github.io/images/data-structure-graph/bipartite-graph2.png

[14-1: 二部图及其判定算法 Bipartite Graphs](https://youtu.be/lyH43SAcyjc)

[演算法筆記 bipartite graph](https://web.ntnu.edu.tw/~algo/BipartiteGraph.html)

### 例題:

[785. Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite)

[886. Possible Bipartition](https://leetcode.com/problems/possible-bipartition)
