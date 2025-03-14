# Binary Search

二分的本質是「二段性」而非「單調性」。

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

## 參考資源

[二分法的二段性、两套模板 和 答案判定](https://writings.sh/post/binary-search)

[3.9 二分查找](https://2xiao.github.io/leetcode-js/leetcode/algorithm/binary_search.html)

## 例題：

[162. Find Peak Element](https://leetcode.com/problems/find-peak-element)

[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array)

[240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii)
