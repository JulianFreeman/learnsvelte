---
title: 检查槽的内容
---

有些情况下，我们需要根据是否有槽内容来控制组件的某些部分。比如说，如果把 `App.svelte` 中的 `<header>` 移除……

```svelte
/// file: App.svelte
---<header slot="header" class="row">
	<span class="color"></span>
	<span class="name">name</span>
	<span class="hex">hex</span>
	<span class="rgb">rgb</span>
	<span class="hsl">hsl</span>
</header>---

<div class="row">
	<span class="color" style="background-color: {row.hex}" />
	<span class="name">{row.name}</span>
	<span class="hex">{row.hex}</span>
	<span class="rgb">{row.rgb}</span>
	<span class="hsl">{row.hsl}</span>
</div>
```

……你就会发现留下了一个丑陋的双边界线，因为 `FilterableList.svelte` 还是渲染了 `<div class="header">`（尽管没有内容）。

我们可以在 `FilterableList.svelte` 中加入一个特殊的 `$$slots` 变量来修正这一点：

```svelte
/// file: FilterableList.svelte
+++{#if $$slots.header}+++
	<div class="header">
		<slot name="header"></slot>
	</div>
+++{/if}+++
```
