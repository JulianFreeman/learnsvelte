---
title: If 代码块
---

HTML 不支持表达 _逻辑_，比如条件或者循环。但 Svelte 可以。

要根据条件渲染某些标记（markup），我们可以用 `if` 代码块包裹起来。让我们在 `count` 达到 `10` 之后显示一些文字：

```svelte
/// file: App.svelte
<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

+++{#if count > 10}
	<p>{count} is greater than 10</p>
{/if}+++
```

尝试一下，更新组件，然后点击按钮。
