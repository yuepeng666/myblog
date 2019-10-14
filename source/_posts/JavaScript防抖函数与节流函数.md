---
title: JavaScript防抖函数与节流函数
date: 2019-02-04 16:25:02
categories: JavaScript
tags: js
---

DOM 操作是非常耗费性能的，如果在监听中，做了一些 DOM 操作，那无疑会给浏览器造成大量性能损失，我们可以通过一些操作来减少 DOM 操作

# 防抖函数

##### 定义：函数调用 n 秒后才会执行，如果函 数在 n 秒内被调用的话则函数不执行，重新计算执行时间(规定一定时间内，时间触发的次数)

```js
//
var timer = false;
window.onscroll = () => {
	// 函数防抖
	clearTimeout(timer); // 清除未执行的代码，重置回初始化状态
	timer = setTimeout(function() {
		console.log('函数防抖');
	}, 300);
};
```

 <!-- more -->

###### 防抖函数封装

```js
/**防抖函数封装**/
function debounce(method, delay) {
	var timer = null;
	return function() {
		var context = this,
			args = arguments;
		clearTimeout(timer);
		timer = setTimeout(function() {
			method.apply(context, args);
		}, delay);
	};
}
```

---

# 节流函数

##### 定义：触发函数事件后，短时间间隔内无法连续调用，只有上一次函数执行后，过了规定的时间间隔，才能进行下一次的函数调用（只允许一个函数在 X 毫秒内执行一次）。

```js
// 函数节流
var canRun = true;
window.onscroll = () => {
	if (!canRun) {
		// 判断是否已空闲，如果在执行中，则直接return
		return;
	}
	canRun = false;
	var timer = setTimeout(() => {
		var scrollTop =
			document.body.scrollTop || document.documentElement.scrollTop;
		console.log('滚动位置：' + scrollTop);
		canRun = true;
	}, 1000);
};
//只有当 canRun 为 ture 时才可执行，当执行完毕时 释放当前任务，允许下一个任务执行
```
