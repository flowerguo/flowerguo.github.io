---
layout:     post
title:      javascript数组操作
description: javascript数组操作
categories: blog
tags: javascript
---

## 数组去重

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

## 数组求最大值

### 第一种方法 
```
var arr = [7, 2, 0, -3, 5];
var max = Math.max.apply(null, arr);

// 由于max()里面参数不能为数组，所以借助apply(funtion,args)方法调用Math.max()，function为要调用的方法，args是数组对象，当function为null时，默认为上文,即相当于apply(Math.max,arr)
```

### 第二种方法 
```
var arr = [7, 2, 0, -3, 5];
var max = arr.sort().reverse()[0];

// 排序默认为升序，reverse()将数组颠倒
```

### 第三种方法 
```
var arr = [7, 2, 0, -3, 5];
function findMax (arr) {
	var max = arr[0];
	for (let i = 0; i < arr.length; i++) {
		if (max < arr[i]) {
			max = arr[i];
		}
	}
	return max;
}

// 循环比值
```

## 数组排序

### 第一种方法 JavaScript sort() 方法
```
var array = [1, 4, -8, -3, 6, 12, 9, 8, -5];
var sortArray = array.sort(function (val1, val2) {
	return val1 - val2;
});
console.log(sortArray);
// [-8, -5, -3, 1, 4, 6, 8, 9, 12]

//sort()方法 按照字母顺序（字符编码的顺序）进行排序的，需要再加一个比较函数
```

### 第二种方法 冒泡排序（从后往前）
```
var array = [1, 4, -8, -3, 6, 12, 9, 8, -5];
function sort (arr) {
	for (var i = 0; i < arr.length; i++) {
		for (var j = 0; j < arr.length-1-j; j++) {
			if (arr[j] > arr[j + 1]) {
				var temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j+1] = temp;
			}
		}
	}
}
sort(array);
console.log(array);

// 比较相邻的元素，如果第一个比第二个大，就交换位置
// 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，最后一个元素是最大数
// 针对所有的元素重复以上的步骤，除了最后一个
```

### 第三种方法 快速排序（递归思想，两边快速排序）
```
var array = [1, 4, -8, -3, 6, 12, 9, 8, -5];
function quickSort (arr) {
	if (arr.lenght <= 1) {
		return arr;
	}
	// 定义中间值的索引 Math.floor 向下取整
	var midIdx = Math.floor(arr.length / 2);
	// 取出中间值
	var temp = arr.splice(index, 1);
	var left = [], right = [];
	for (var i = 0; i < arr.length; i++) {
		if (arr[i] < temp) {
			left.push(arr[i]);
		} else {
			right.push(arr[i]);
		}
	}
	return quickSort(left).concat(temp, quickSort(right));
}
console.log(quickSort(array));
```

### 第四种方法 插入排序
```
var array = [1, 4, -8, -3, 6, 12, 9, 8, -5];
function insertSort (arr) {
	for (var i = 0; i < arr.length; i++) {
		if (arr[i] < arr[i - 1]) {
			var temp = arr[i];
			var j = i - 1;
			while (j >= 0 && temp < arr[j]) {
				arr[j + 1] = arr[j];
				j --;
			}
			arr[j+1] = temp;
		}
	}
}
insertSort(array);
console.log(array);

// 从第一个元素开始，该元素可以认为已被排序
// 取出下一个元素，在已经排序的元素序列中扫描
// 如果该元素（已排序）大于新元素，将该元素一到下一位置
// 重复上一步骤，直到找到已排序的元素小于或者等于新元素的位置
// 将新元素插入到下一位置中
```

### 第四种方法 选择排序
```
var array = [1, 4, -8, -3, 6, 12, 9, 8, -5];
function selectSort (arr) {
	for (var i = 0; i < arr.length; i++) {
		var min = arr[i];
		var minIndex = i;
		for (var j = i + 1; j < arr.length; j++) {
			if (min > arr[j]) {
				min = arr[j];
				minIndex = j;
			}
		}
		arr.splice(i, 0, min);
		arr.splice(minIndex+1, 1);
	}
}
selectSort(array);
console.log(array);

// 在未排序序列中找到最小元素
// 并存放到排序序列的起始位置
// 从剩余未排序元素中寻找最小元素
// 然后放到已排序序列的末端
```

## 数组操作题目
有一个有序、不连续、不重复的数组 [12, 37, 42, 56, 69, 85 ...]，有一个随机数 x，求 x 在数组中的位置，如果存在返回 x 的位置，不存在返回 -1
```
function findx (arr, x) {
	var midLength = parseInt(arr.length/2),
			midVal = arr[midLength],
			start = x < midVal ? 0 : midLength,
			end = x < midVal ? midLength : arr.length;

	for (let i = start; i < end; i ++) {
		if (x == arr[i]) {
			return i
		}
	}
	return -1
}
```