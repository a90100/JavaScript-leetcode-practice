# Binary Tree

> Tree is special form of graph.

## BFS(Breadth-First Search)

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

### 例題:

[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)

## 前、中、後序遍歷比較圖

https://imgur.com/a/RugKzaw

## Preorder Traversal(前序遍歷)

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

### 例題:

[114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)

## Inorder Traversal(中序遍歷)

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

### 例題:

[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst)

[173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator)

## Postorder traversal(後序遍歷)

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

## Binary Search Tree

1. 若任意節點的左子樹不空，則左子樹上所有節點的值均小於它的根節點的值
2. 若任意節點的右子樹不空，則右子樹上所有節點的值均大於它的根節點的值
3. 任意節點的左、右子樹也分別為二元搜尋樹
4. 二元搜尋樹相比於其他資料結構的優勢在於尋找、插入的時間複雜度較低，平均為 `O(log n)`。

### 例題:

[450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst)

> 思考: 刪除節點後的更新情況有哪幾種?

## Complete Binary Tree

各層節點全滿，除了最後一層，最後一層節點全部靠左。

### 例題:

[222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes)
