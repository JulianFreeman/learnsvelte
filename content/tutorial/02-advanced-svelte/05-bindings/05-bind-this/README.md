---
title: This
---

在 [之前的练习](onmount) 中，我们学习了如何使用 `onMount` 生命周期函数绘制画布。

但是那个例子中有个小 bug，因为使用了 `document.querySelector('canvas')`，所以它总是会返回页面上找到的第一个 `canvas` 元素，有时候这可能并不是你需要的那个。

现在，我们可以使用一个只读的 `this` 绑定来获取元素的索引：

```js
/// file: App.svelte
+++let canvas;+++

onMount(() => {
	---const canvas = document.querySelector('canvas')---
	const context = canvas.getContext('2d');

	let frame = requestAnimationFrame(function loop(t) {
		frame = requestAnimationFrame(loop);
		paint(context, t);
	});

	return () => {
		cancelAnimationFrame(frame);
	};
});
```

```svelte
/// file: App.svelte
<canvas
	+++bind:this={canvas}+++
	width={32}
	height={32}
></canvas>
```

注意，在组件初始化之前，`canvas` 都是 `undefined` 的。
