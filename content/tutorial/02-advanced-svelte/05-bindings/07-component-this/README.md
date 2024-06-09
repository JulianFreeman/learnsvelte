---
title: 绑定到组件实例
---

就如同你可以绑定到 DOM 元素一样，你也可以使用 `bind:this` 绑定到组件实例。

在少数情况下这的确有用，特别是你需要通过程序与组件交互的时候（而非提供一些更新的属性）。回顾一下不久之前的 [一个练习](actions)，在这个画布应用中，能添加一个清除画布的按钮会更好。

首先，让我们从 `Canvas.svelte` 导出一个函数：

```svelte
/// file: Canvas.svelte
export let color;
export let size;

+++export function clear() {
	context.clearRect(0, 0, canvas.width, canvas.height);
}+++
```

然后，创建一个指向组件实例的引用：

```svelte
/// file: App.svelte
<script>
	import Canvas from './Canvas.svelte';
	import { trapFocus } from './actions.js';

	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet', 'white', 'black'];
	let selected = colors[0];
	let size = 10;

	let showMenu = true;
	+++let canvas;+++
</script>

<div class="container">
	<Canvas +++bind:this={canvas}+++ color={selected} size={size} />
```

最后，添加一个调用 `clear` 函数的按钮：

```svelte
/// file: App.svelte
<div class="controls">
	<button class="show-menu" on:click={() => showMenu = !showMenu}>
		{showMenu ? 'close' : 'menu'}
	</button>

+++	<button on:click={() => canvas.clear()}>
		clear
	</button>+++
</div>
```