---
title: 自定义存储
---

只要一个对象正确地实现了 `subscribe` 方法，那它就是一个 store，除此之外，没有任何要求。因此要创建特定领域逻辑的自定义存储是很简单的。

比如说，我们之前例子中的 `count` 这个 store 可以包含 `increment`、`decrement` 和 `reset` 方法而避免暴露 `set` 和 `update`：

```js
/// file: stores.js
function createCount() {
	const { subscribe, set, update } = writable(0);

	return {
		subscribe,
		increment: () => +++update((n) => n + 1)+++,
		decrement: () => +++update((n) => n - 1)+++,
		reset: () => +++set(0)+++
	};
}
```
