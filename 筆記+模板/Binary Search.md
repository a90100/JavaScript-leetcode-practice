# Binary Search

二分的本質是「二段性」而非「單調性」，只要一段滿足某個性質，另外一段不滿足某個性質，就可以用「二分」。

可以參考 1011. Capacity To Ship Packages Within D Days 和 1482. Minimum Number of Days to Make m Bouquets 的筆記，可以更了解二段性質。

在數學中，單調性指的是函數在特定區間上的增減趨勢。如果一個函數在一個區間內，隨著自變數的增大，因變數也增大，則稱該函數為單調遞增函數；反之，如果隨著自變數的增大，因變數減小，則稱該函數為單調遞減函數。單調性是函數的重要性質之一，它描述了函數在定義域上的整體變化趨勢。

#### 單調遞增函數：

對於定義域上的任意兩個自變數值 x1 和 x2，如果 x1 < x2 且 f(x1) < f(x2)，則稱 f(x) 在該區間上是單調遞增的。

#### 單調遞減函數：

對於定義域上的任意兩個自變數值 x1 和 x2，如果 x1 < x2 且 f(x1) > f(x2)，則稱 f(x) 在該區間上是單調遞減的。

舉例：410. Split Array Largest Sum 解題思路中，子陣列數目和總和的關係。

> 二分搜尋常見的題目需求：非負整數、要求最大化最小值或最小化最大值。

## 題目需求轉換思考

假設陣列有排序，要求 `<= target` 的值，其實可以看做求第一個 `> target` 的值的前一個值，也可以看做求第一個 `>= target + 1` 的值的前一個值。

## 基本模板

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

## 變形模板: 查找第一個值等於給定值的元素

```javascript
var search = function (nums, target) {
  let l = 0;
  let r = nums.length - 1;
  let index = -1;

  while (l <= r) {
    const mid = Math.floor((l + r) / 2);
    if (nums[mid] === target) {
      index = mid;
      r = mid - 1;
    } else if (nums[mid] > target) {
      r = mid - 1;
    } else {
      l = mid + 1;
    }
  }
  return index;
};
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 2); // 11
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 7); // -1
```

## 變形模板: 查找最後一個值等於給定值的元素

```javascript
var search = function (nums, target) {
  let l = 0;
  let r = nums.length - 1;
  let index = -1;

  while (l <= r) {
    const mid = Math.floor((l + r) / 2);
    if (nums[mid] === target) {
      index = mid;
      l = mid + 1;
    } else if (nums[mid] > target) {
      r = mid - 1;
    } else {
      l = mid + 1;
    }
  }
  return index;
};
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 2); // 21
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 7); // -1
```

## 變形模板: 查找第一個大於等於給定值的元素

```javascript
var search = function (nums, target) {
  let l = 0;
  let r = nums.length - 1;

  while (l <= r) {
    const mid = Math.floor((l + r) / 2);
    if (nums[mid] < target) {
      l = mid + 1;
    } else {
      if (mid === 0 || nums[mid - 1] < target) return mid;
      r = mid - 1;
    }
  }
  return -1; // nums 所有元素都比給定值小
};
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 2); // 11
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 7); // -1
```

## 變形模板: 查找大於等於給定值的最小元素索引

```javascript
var search = function (nums, target) {
  let l = 0;
  let r = nums.length - 1;

  while (l < r) {
    const mid = Math.floor((l + r) / 2);
    if (nums[mid] < target) {
      l = mid + 1; // mid 肯定不是要找的值，所以略過
    } else {
      r = mid; // mid 可能是要找的值，所以不略過
    }
  }
  return nums[l] >= target ? l : -1; // -1 代表整個陣列都比 target 小
};
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 7); // -1
```

> 1300. Sum of Mutated Array Closest to Target 有用到

## 變形模板: 查找最後一個小於等於給定值的元素

```javascript
var search = function (nums, target) {
  let l = 0;
  let r = nums.length - 1;

  while (l <= r) {
    const mid = Math.floor((l + r) / 2);
    if (nums[mid] > target) {
      r = mid - 1;
    } else {
      if (mid === nums.length - 1 || nums[mid + 1] > target) return mid;
      l = mid + 1;
    }
  }
  return -1; // nums 所有元素都比給定值大
};
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 2); // 21
search([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6], 7); // 31
```

## 變形模板: 查找第一個比給定值的元素大的元素

參考 744. Find Smallest Letter Greater Than Target

```javascript
var nextGreatestLetter = function (letters, target) {
  let l = 0;
  let r = letters.length - 1;

  while (l < r) {
    const mid = Math.floor((l + r) / 2);

    if (letters[mid] > target) {
      r = mid; // 符合 letters[mid] > target 的條件，而 letters[mid] 本身有可能就是題目要的答案，所以選擇逐步逼近 l 指針
    } else {
      l = mid + 1;
    }
  }

  return letters[r] > target ? letters[r] : -1; // 如果最後一個元素比 target 大，則返回該元素，否則返回 -1
};
```

## 參考資源

[二分法的二段性、两套模板 和 答案判定](https://writings.sh/post/binary-search)

[3.9 二分查找](https://2xiao.github.io/leetcode-js/leetcode/algorithm/binary_search.html)

## 例題：

[162. Find Peak Element](https://leetcode.com/problems/find-peak-element)

[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array)

[240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii)
