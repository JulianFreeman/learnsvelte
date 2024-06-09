---
title: beforeUpdate 和 afterUpdate
---

`beforeUpdate` 函数负责的是在 DOM 更新前发生什么，`afterUpdate` 则负责更新后发生什么。两个函数用来在 DOM 与数据同步时运行一些代码。

对于一些很难通过纯粹的状态驱动的方式执行的任务，这两个函数会很有用。比如更新一个元素的滚动条位置。

这个 [Eliza](https://en.wikipedia.org/wiki/ELIZA) 聊天机器人用起来有点烦人，因为你每次都需要手动滚动聊天窗口。让我们解决这个问题。

```js
/// file: App.svelte
let div;
+++let autoscroll = false;+++

beforeUpdate(() => {
+++	if (div) {
		const scrollableDistance = div.scrollHeight - div.offsetHeight;
		autoscroll = div.scrollTop > scrollableDistance - 20;
	}+++
});

afterUpdate(() => {
+++	if (autoscroll) {
		div.scrollTo(0, div.scrollHeight);
	}+++
});
```

要注意的是，`beforeUpdate` 会在组件初始化之前运行，因此我们需要先检查 `div` 是否存在，再决定是否读取其属性。
