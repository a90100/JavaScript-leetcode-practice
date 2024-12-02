# Take K of Each Character From Left and Right

## 解題程式碼

```javascript
var takeCharacters = function (s, k) {
  const abcMap = { a: 0, b: 0, c: 0 };
  let mins = s.length;
  let l = 0;

  for (let i = 0; i < s.length; i++) {
    abcMap[s[i]]++;
  }
  if (abcMap.a < k || abcMap.b < k || abcMap.c < k) return -1;

  for (let i = 0; i < s.length; i++) {
    abcMap[s[i]]--;

    while (abcMap[s[i]] < k) abcMap[s[l++]]++;
    mins = Math.min(mins, s.length - (i - l + 1));
  }
  return mins;
};
```

## 解題思路、演算法

先計算 s 字串出現 a、b、c 的個數，若 a、b、c 任一小於 k，則直接回傳 -1。

接下來維護一個 window，盡可能讓 window 長度更長，代表移出字元少，

若 `a < k || b < k || c < k` 時，須調整 window。

## 解法的時間、空間複雜度

時間複雜度: O(n)
空間複雜度: O(1)

## 參考資料

[Take K of Each Character From Left and Right - Leetcode - Python](https://youtu.be/QzcxeJZByNM)
