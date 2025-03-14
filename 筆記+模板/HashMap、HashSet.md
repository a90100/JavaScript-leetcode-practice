# HashMap、HashSet

假設有要處理重複字串/數字的情境，應該要想到這兩個資料結構，例如 677. Map Sum Pairs 也能用 hashMap。

## 模板：將陣列元素存入 hashMap

```javascript
const hashMap = new Map();

for (let i = 0; i < s.length; i++) {
  hashMap.set(s[i], (hashMap.get(s[i]) || 0) + 1);
}

// 更快的做法：lodash.js 的 _.countBy，不過是物件
const hashMap = _.countBy(s);

// for (let i = 0; i < s.length; i++) {
//     if (hashMap[s[i]] === 1) return i; // 用物件的方式取 value
// }
```

## 做 mapping 的內建函式有以下這些

都可以用 forEach 做 mapping。

### 例題:

[347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)

### Map.prototype.entries()、keys()、values()

```javascript
for (var [key, value] of hashMap) {
  // for of 可以不用加 entries()，等於以下 for of
}

for (var [key, value] of hashMap.entries()) {
  // ...
}

for (var key of hashMap.keys()) {
  // ...
}

for (var value of hashMap.values()) {
  // ...
}

// 物件的寫法：
for (const [key, value] of Object.entries(obj1)) {
  // ...
}

// 如果傳入陣列，會印出索引
for (const [key, value] of Object.entries(array)) {
  // ...
}

// 例如：
for (const [key, value] of Object.entries([1, 2])) {
  console.log(key, value);
}

// 0 1
// 1, 2
```

## 將取到的 keys、values 轉成陣列

```javascript
const map = new Map();

map.set(1, '1');
map.set(2, '2');

console.log(Array.from(map.values()));

// 或是
console.log([...map.values()]);

const mySet = new Set([1, 1, 2, 3, 4, 4, 5, 6, 5]);
let myArr = Array.from(mySet); // [1, 2, 3, 4, 5, 6]
```

## 更新 HashMap

如果 value 是陣列，用上面這種寫法而不是 Spread Operator

```javascript
// O(1)
const values = hashMap.get(key) || [];
values.push(newObj);
hashMap.set(key, values);

// O(n)
hashMap.set(key, hashMap.get(key) ? [...hashMap.get(key), newObj] : [newObj]);
```

## HashMap 轉陣列、陣列轉 HashMap、HashMap 轉物件、物件轉 HashMap、HashMap 轉 JSON、JSON 轉 HashMap

參考 [LeetCode-JS](https://2xiao.github.io/leetcode-js/book/hash.html#%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E7%9A%84%E4%BA%92%E7%9B%B8%E8%BD%AC%E6%8D%A2)

## 實際上 hashMap、hashSet 的 set、add、get 時間複雜度最差為 O(n)，頻繁雜湊衝突時

可參考 3418. Maximum Amount of Money Robot Can Earn 的筆記

## 如果從 hashMap 取出陣列，要以複製的形式產生新陣列，不然會有 reference 的問題，在 LeetCode 上會跳出和記憶體相關的提示訊息。

### 例題:

[737. Sentence Similarity II](https://leetcode.com/problems/sentence-similarity-ii)

筆記中的解法：

```javascript
const queue = [...(similarMap?.get(s1[i]) ?? [])];
// const queue = similarMap.get(s1[i]) ?? []; 這樣寫不對，物件 by reference 問題
```
