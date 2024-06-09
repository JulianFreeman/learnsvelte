---
title: onMount
---

每一个组件都有一个 _生命周期_，从组件创建时起，到组件销毁时止。Svelte 有很多函数可以让我们在生命周期的某些关键阶段执行代码。最常用的一个就是 `onMount`，在组件第一次渲染到 DOM 时调用。

在本节练习中，我们有一个 `canvas` 元素，并使用 `gradient.js` 中的 `paint` 函数来制作动画。首先从 `svelte` 中导入 `onMount` 函数：

```svelte
/// file: App.svelte
<script>
	+++import { onMount } from 'svelte';+++
	import { paint } from './gradient.js';
</script>
```

然后添加一个在组件初始化后调用的回调函数：

```svelte
/// file: App.svelte
<script>
	import { onMount } from 'svelte';
	import { paint } from './gradient.js';

+++	onMount(() => {
		const canvas = document.querySelector('canvas');
		const context = canvas.getContext('2d');+++

+++		requestAnimationFrame(function loop(t) {
			requestAnimationFrame(loop);
			paint(context, t);
		});
	});+++
</script>
```

> 在 [之后的一节练习](bind-this) 中，我们会学习不用 `document.querySelector` 也能获取元素的索引。

目前为止一切尚好。你应该能看到 Svelte 的 logo 上有轻微的此起彼伏的颜色。但这里有一个问题：这个循环在组件被销毁后依然还会运行。要解决这个问题，我们需要 `onMount` 返回一个清理函数：

```js
/// file: App.svelte
onMount(() => {
	const canvas = document.querySelector('canvas');
	const context = canvas.getContext('2d');

	+++let frame =+++ requestAnimationFrame(function loop(t) {
		+++frame =+++ requestAnimationFrame(loop);
		paint(context, t);
	});

+++	return () => {
		cancelAnimationFrame(frame);
	};+++
});
```
