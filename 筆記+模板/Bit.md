# Bit

## 位元運算特性

1. 優點是速度快，減少時間複雜度，缺點是不直觀且只支持整數運算
2. 原本 JavaScript 的數值類型（Number）是 64 位元浮點數（IEEE 754 double-precision floating point），進行位運算時會將操作數轉換為 32 位元的帶符號整數（signed 32-bit integers），也就是 65 位浮點數 => 32 位整數 => 進行位運算

根據第二點，在轉換後，若超過 32 位，超過的部分會被捨棄，取低位 32 bit，一般會被捨棄會是超過 -2^31 ~ 2^31-1 的數字，或是小數的部分，所以才會有第一點的缺點。

```
      Before: 11100110111110100000000000000110000000000001
      After:              10100000000000000110000000000001
```

## [Bitwise AND (&)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_AND)

可以計算兩個數字其二進位數的每個位元是否都為一然後輸出

```javascript
const a = 5; // 00000000000000000000000000000101
const b = 3; // 00000000000000000000000000000011

console.log(a & b); // 00000000000000000000000000000001
```

## [Bitwise XOR (^)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_XOR)

兩個數字轉成二進位後，兩個數相同位元只要不是都是 1 或 0 就輸出 1

> 特性 兩個相同數字做 ^ 會變成 0，可練習 [136. Single Number](https://leetcode.com/problems/single-number)

```javascript
const a = 5; // 00000000000000000000000000000101
const b = 3; // 00000000000000000000000000000011

console.log(a ^ b); // 00000000000000000000000000000110
// Expected output: 6

const a = 5; // 00000000000000000000000000000101
const b = 5; // 00000000000000000000000000000101

console.log(a ^ b); // 00000000000000000000000000000000
```

## (左、右)位移位運算子、無符號右位移運算子

- [Left shift (<<)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Left_shift)
- [Right shift (>>)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Right_shift)
- [Unsigned right shift (>>>)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Unsigned_right_shift)

```javascript
const a = 5; // 00000000000000000000000000000101
const b = 2; // 00000000000000000000000000000010

console.log(a << b); // 00000000000000000000000000010100
// Expected output: 20
//-----------------------------------------------------------
const a = 5; //  00000000000000000000000000000101
const b = 2; //  00000000000000000000000000000010
const c = -5; //  11111111111111111111111111111011

console.log(a >> b); //  00000000000000000000000000000001
// Expected output: 1

console.log(c >> b); //  11111111111111111111111111111110
// Expected output: -2
//-----------------------------------------------------------
const a = 5; //  00000000000000000000000000000101
const b = 2; //  00000000000000000000000000000010
const c = -5; //  11111111111111111111111111111011

console.log(a >>> b); //  00000000000000000000000000000001
// Expected output: 1

console.log(c >>> b); //  00111111111111111111111111111110，差異在整個數字右移後，前面補上 b 個 0
// Expected output: 1073741822
```

## 取代 Math.pow

```javascript
// 設 n 為 1~無限大值，則 1 << n 可以得到 2^n 值
console.log(1 << n);
console.log(1 << 5); // 32
```
