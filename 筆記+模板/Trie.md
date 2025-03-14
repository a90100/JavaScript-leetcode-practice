# Trie

## 模板

取自 208. Implement Trie (Prefix Tree) ：

```javascript
var Trie = function () {
  this.trie = {};
};

Trie.prototype.insert = function (word) {
  let curObj = this.trie;
  for (let i = 0; i < word.length; i++) {
    if (!curObj[word[i]]) curObj[word[i]] = {};
    curObj = curObj[word[i]];
  }
  curObj.isWord = true;
};

Trie.prototype.search = function (word) {
  let curObj = this.trie;
  for (let i = 0; i < word.length; i++) {
    if (!curObj[word[i]]) return false;
    curObj = curObj[word[i]];
  }
  return !!curObj.isWord;
};

Trie.prototype.startsWith = function (prefix) {
  let curObj = this.trie;
  for (let i = 0; i < prefix.length; i++) {
    if (!curObj[prefix[i]]) return false;
    curObj = curObj[prefix[i]];
  }
  return true;
};

// 使用範例
```
