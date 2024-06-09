---
title: 组件样式
---

有时候，你需要更改一个子组件内的样式，比如说我们希望这些盒子是红色、绿色和蓝色的。

其中一个办法是使用 `:global` CSS 修饰器，可以无差别影响到其他组件内的任意目标元素：

```svelte
/// file: App.svelte
<style>
	.boxes :global(.box:nth-child(1)) {
		background-color: red;
	}

	.boxes :global(.box:nth-child(2)) {
		background-color: green;
	}

	.boxes :global(.box:nth-child(3)) {
		background-color: blue;
	}
</style>
```

但是这样做显然 _不_ 是很好。一方面，有点繁琐，另一方面，太脆弱，任何对 `Box.svelte` 实现细节的更改都可能会破坏这个选择器。

最主要的是，这太粗暴了。组件应该能够自行决定哪些样式可以从外部控制，就跟它们可以决定哪些属性可以暴露出去一样。`:global` 只能作为最后孤注一掷的手段使用。

在 `Box.svelte` 中，修改 `background-color` 以便由 [CSS 自定义属性](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) 控制其值：

```svelte
/// file: Box.svelte
<style>
	.box {
		width: 5em;
		height: 5em;
		border-radius: 0.5em;
		margin: 0 0 1em 0;
		background-color: +++var(--color, #ddd)+++;
	}
</style>
```

任何父级元素（比如 `<div class="boxes">`）都可以设置 `--color` 的值，但是我们也可以分别设置在组件上：

```svelte
/// file: App.svelte
<div class="boxes">
	<Box +++--color="red"+++ />
	<Box +++--color="green"+++ />
	<Box +++--color="blue"+++ />
</div>
```

这些值也可以是动态的，就跟其他任何属性（attribute）一样。

这个特性的原理是在需要的时候给每个组件包上一层 `<div style="display: contents">`，然后添加上自定义的属性。
