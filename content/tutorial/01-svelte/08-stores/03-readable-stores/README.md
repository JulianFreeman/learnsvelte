---
title: 可读存储
---

不是所有的 store 都应该被任何获取到它的对象改写。比如说你可能会用一个 store 来存储鼠标位置或者用户的地理位置，这样的值不应该从外部被修改。对于这种情况，我们有 _可读_ 存储。

打开 `stores.js`，`readable` 函数的第一个参数是一个初始值，如果没有初始值的话也可以设为 `null` 或者 `undefined`。第二个参数是一个 `start` 函数，它接收一个 `set` 回调函数并返回一个 `stop` 函数。`start` 函数会在这个 store 收到第一个订阅者时调用，`stop` 函数会在最后一个订阅者取消订阅时调用。

```js
/// file: stores.js
export const time = readable(+++new Date()+++, function start(set) {
+++	const interval = setInterval(() => {
		set(new Date());
	}, 1000);+++

	return function stop() {
		+++clearInterval(interval);+++
	};
});
```
