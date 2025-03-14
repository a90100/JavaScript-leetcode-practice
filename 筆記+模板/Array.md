# Array

## 競賽模板

### for 迴圈

```javascript
const res = [];

for (let i = 0; i < ?.length; i++) {};

return res;

// 不會使用到索引的情況，用 for of 更好
for (let query of queries) {};
```

### 建立 2D 陣列

```javascript
const twoDArr = new Array(rows).fill().map(() => new Array(cols).fill(0));
```

[How can I create a two-dimensional array in JavaScript?](https://sentry.io/answers/how-can-i-create-a-two-dimensional-array-in-javascript/)

## 解陣列問題常用的招式

- 思考是否陣列有先排序
- 思考將所有元素加總後的值有沒有用

## 處理循環陣列

善用除法 / 取模。

另外一種做法是做兩個相同陣列的拼接。

往後走：`(currentIndex + k) % n`

往前走：`(currentIndex - k + n) % n`

### 例題：

[1652. Defuse the Bomb](https://leetcode.com/problems/defuse-the-bomb)

[3379. Transformed Array](https://leetcode.com/problems/transformed-array)

## 判斷是否四個點能組成矩形

若有兩對 x 相同的點，形成兩個垂直的邊 且 也有兩對 y 相同的點，形成兩個水平的邊，則可以組成矩形。

例如：`[1, ?], [1, ?], [3, ?], [3, ?]` 且 `[?, 2], [?, 2], [?, 4], [?, 4]` 則可以組成。

組合範例：`[1, 2], [1, 4], [3, 2], [3, 4]`。

## Prefix Sum

[Prefix Sum（前綴和）概念](https://claire-chang.com/2023/05/04/prefix-sums%EF%BC%88%E5%89%8D%E7%B6%B4%E5%92%8C%EF%BC%89%E6%A6%82%E5%BF%B5/)

求**區段和**的題目，可以聯想到此演算法。

### Prefix Sum LeetCode 題目列表

[Prefix Sum](https://leetcode.com/tag/prefix-sum/)

## Difference Array 差分陣列(數組)

適用情境為 頻繁對原始陣列的某個範圍進行增減，一般會宣告一個陣列 diff 去記錄。

參考文章：[小而美的算法技巧：差分数组](https://labuladong.online/algo/data-structure/diff-array/)

### 例題：

[3355. Zero Array Transformation I](https://leetcode.com/problems/zero-array-transformation-i)
