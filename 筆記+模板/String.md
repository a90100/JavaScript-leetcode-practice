# String

## KMP 演算法

[KMP 演算法筆記](https://ithelp.ithome.com.tw/articles/10353360)

## `includes()` worst case 的時間複雜度是 O(l^2)，avg case 是 O(l)

```javascript
if (words[j].includes(words[i])) // 假設 words[j] 長度為 L, words[i] 長度為 M
```

1. 在 `words[j]`（長度 L）中找到 `words[i]`（長度 M）
2. 它會從 `words[j]` 的頭開始，逐個嘗試匹配 `words[i]`
3. 如果匹配成功，則時間複雜度為 O(L)（因為最好情況下，它只需要掃過一次 `words[j]`）
4. 如果 `words[i]` 和 `words[j]` 在許多位置部分匹配但不完全匹配，最壞情況可能達到 `O(L * M)`（暴力匹配）

```javascript
let text = 'aaaaaaaaaaaaaaaab'; // 長度 L
let pattern = 'aaaaaaaaaaaaaaac'; // 長度 M（幾乎相同，但最後一個字母不同）

text.includes(pattern);
```
