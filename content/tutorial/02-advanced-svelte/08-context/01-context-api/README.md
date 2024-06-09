---
title: setContext 和 getContext
---

Context API 提供了一种可以让组件之间相互通信的方法，而不用来回用属性传递数据或者函数，或者派发一堆的事件。这是一个高级特性，不过很有用。这本例中，我们将会使用 Context API 重建生成式艺术的先驱之一，George Nees 创作的 [Schotter](https://collections.vam.ac.uk/item/O221321/schotter-print-nees-georg/)。

在 `Canvas.svelte` 中，有一个 `addItem` 函数用来向画布中添加元素。我们可以用 `setContext` 来让 `<Canvas>` 的子组件（比如 `<Square>`）也能获取这个函数：

```svelte
/// file: Canvas.svelte
<script>
	import { +++setContext+++, afterUpdate, onMount, tick } from 'svelte';

	// ...

	onMount(() => {
		ctx = canvas.getContext('2d');
	});

+++	setContext('canvas', {
		addItem
	});+++

	function addItem(fn) {...}

	function draw() {...}
</script>
```

在子组件中，我们现在可以用 `getContext` 来获取这个 Context 了：

```svelte
/// file: Square.svelte
<script>
	+++import { getContext } from 'svelte';+++

	export let x;
	export let y;
	export let size;
	export let rotate;

	+++getContext('canvas').addItem(draw);+++

	function draw(ctx) {...}
</script>
```

目前为止，一切尚……有点无聊。让我们向表格中加点随机性：

```svelte
/// file: App.svelte
<div class="container">
	<Canvas width={800} height={1200}>
		{#each Array(12) as _, c}
			{#each Array(22) as _, r}
				<Square
					x={180 + c * 40+++ + jitter(r * 2)+++}
					y={180 + r * 40+++ + jitter(r * 2)+++}
					size={40}
					+++rotate={jitter(r * 0.05)}+++
				/>
			{/each}
		{/each}
	</Canvas>
</div>
```

如同 [生命周期函数](/tutorial/onmount) 一样，`setContext` 和 `getContext` 必须在组件初始化期间被调用。（Context 的 key（此例中的 `'canvas'`）可以是任意值，包括非字符串，这对于控制谁可以获取这个 Context 很有用。）

那你的 Context 对象也可以包含任意值，包括 stores。这允许你向子组件传递一些会随着时间变化的值：

```js
/// no-file
// in a parent component
import { setContext } from 'svelte';
import { writable } from 'svelte/store';

setContext('my-context', {
	count: writable(0)
});
```
```js
/// no-file
// in a child component
import { getContext } from 'svelte';

const { count } = getContext('my-context');

$: console.log({ count: $count });
```
