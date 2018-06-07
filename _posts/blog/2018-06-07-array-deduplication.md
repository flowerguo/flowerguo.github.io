---
layout:     post
title:      javascript数组去重
description: javascript数组去重
categories: blog
tags: javascript
---

### 第一种方法 时间复杂度为 O(n^2)

```JavaScript
function uniq (arr) {
	var result = [];
	var flag = true;
	for (let i = 0; i < arr.length; i++) {
		flag = true;
		for (let j = 0; j < result.length; j++) {
			if (result[j] === arr[i]) {
				flag = false;
			}
		}
		if (flag) {
			result.push(arr[i]);
		}
	}
	return result;
}
```

### 第二种方法 indexOf() 与 filter结合使用 时间复杂度为 O(n)

```JavaScript
function uniq (arr) {
	return arr.filter(function(item, index, array) {
		return arr.indexOf(item) === index;
	});
}
```      
        
### 第三种方法 借助对象，没有区分类型，例如2和“2” 时间复杂度为 O(n)

```JavaScript
function uniq (arr) {
	var result = [];
	var obj = {};
	for (let i = 0; i < arr.length; i++) {
		if(!obj[arr[i]]) {
			result.push(arr[i]);
			obj[arr[i]] = 1;
		}
	}
	return result
}
``` 

### 第四种方法 ES6方法 Set方法 不会发生类型转换

```JavaScript
[...new Set([1,2,3,4,1,1,2,3,2])]
输出：[1, 2, 3, 4]
``` 