---
title: MDN阅读笔记
copyright: true
date: 2019-04-02 11:14:51
tags:
---

[MDN Web Doc](https://developer.mozilla.org/zh-CN/)

# 新世界的大门

[Web API](https://developer.mozilla.org/zh-CN/docs/Web/API)
[Firefox OS](https://zh.wikipedia.org/wiki/Firefox_OS)
[canvas 教程](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/)(中文没有在线演示)
[IndexedDB](https://developer.mozilla.org/zh-CN/docs/Web/API/IndexedDB_API)
[await](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await)

## JS Number 合集

[JS Number](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number) MAX/MIN SAFE INTEGER MIN_VALUE
[JS 浮点](https://en.wikipedia.org/wiki/Double-precision_floating-point_format#JavaScript)

```
console.log(Number.MAX_SAFE_INTEGER); //9007199254740991
console.log(Number.MIN_SAFE_INTEGER); //-9007199254740991
```

## JS Object 合集

[apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

## JS Array

[MDN Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

[Array.map()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

Freecode Camp 题:
[Return Largest Numbers in Arrays](https://learn.freecodecamp.org/javascript-algorithms-and-data-structures/basic-algorithm-scripting/return-largest-numbers-in-arrays)
[Answer](https://guide.freecodecamp.org/certifications/javascript-algorithms-and-data-structures/basic-algorithm-scripting/return-largest-numbers-in-arrays/)
当你还在复杂的 for 循环的时候

```
function largestOfFour(arr) {
  var results = [];
  for (var n = 0; n < arr.length; n++) {
    var largestNumber = arr[n][0];
    for (var sb = 1; sb < arr[n].length; sb++) {
      if (arr[n][sb] > largestNumber) {
        largestNumber = arr[n][sb];
      }
    }

    results[n] = largestNumber;
  }

  return results;
}
```

看到这样的骚操作

```
function largestOfFour(arr) {
  return arr.map(Function.apply.bind(Math.max, null));
}
```

大概会惊讶于竟然有如此简单明了的写法而很鄙视自己之前写的代码吧

## Web 储存合集

Local Storage
Session Storage
IndexedDB
Web SQL
Cookies
