---
title: 命名槽
---

上一个例子中包含一个 _默认的槽_，会渲染一个组件的直接子组件。有时候你需要对放置子组件有更多的把控，这时候就需要 _命名槽_。

在 `App.svelte` 中，我们渲染了一个包含 `<span slot="telephone">` 以及另外两个 `company` 和 `address` 的 `<Card>` 组件。让我们把相应的命名槽加入到 `Card.svelte` 中：

```svelte
/// file: Card.svelte
<div class="card">
+++	<header>
		<slot name="telephone"></slot>
		<slot name="company"></slot>
	</header>+++

	<slot></slot>

+++	<footer>
		<slot name="address"></slot>
	</footer>+++
</div>
```

我们需要对 `App.svelte` 中的 `<small>` 元素添加一些样式，这样它就能独占一行。`<Card>` 的内容继承了来自 `Card.svelte` 的样式，比如说 `font-family`（卡片的内容来自 [这个视频](https://www.youtube.com/watch?v=aZVkW9p-cCU)），但其他的需要遵守一般的作用域规则，因此我们需要在 `App.svelte` 中给 `<small>` 添加样式，因为这才是这个元素所在的文件：

```svelte
/// file: App.svelte
<style>
	main {
		display: grid;
		place-items: center;
		height: 100%;
		background: url(./wood.svg);
	}

+++	small {
		display: block;
		font-size: 0.6em;
		text-align: right;
	}+++
</style>
```

或者我们也可以在 `Card.svelte` 内使用 `:global` 修饰器对 `.card` 内的所有 `small` 元素施加样式：

```svelte
/// file: Card.svelte
<style>
	/* ... */

	+++.card :global(small) {
		display: block;
		font-size: 0.6em;
		text-align: right;
	}+++
</style>
```
