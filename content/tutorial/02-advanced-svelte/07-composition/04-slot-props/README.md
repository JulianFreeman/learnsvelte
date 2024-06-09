---
title: 槽属性
---

组件可以通过 _槽属性（slot props）_ 把数据 _传回_ 它们槽里的内容。在本例中，我们有一个 CSS 名称颜色的列表，在 `input` 元素内输入内容可以过滤列表。

现在每一行都显示的 `AliceBlue`，尽管这个颜色挺喜人的，但这不是我们想要的。

打开 `FilterableList.svelte`，列表中的每一个被过滤出来的元素都会被 `slot` 渲染。向这个槽中传递数据：

```svelte
/// file: FilterableList.svelte
<div class="content">
	{#each data.filter(matches) as item}
		<slot +++{item}+++></slot>
	{/each}
</div>
```

（在这里，`{item}` 是 `item={item}` 的简写。）

然后另一边，使用 `let:` 标志将数据暴露给槽里的内容。

```svelte
/// file: App.svelte
<FilterableList
	data={colors}
	field="name"
	+++let:item={row}+++
>
	<div class="row">
		<span class="color" style="background-color: {row.hex}" />
		<span class="name">{row.name}</span>
		<span class="hex">{row.hex}</span>
		<span class="rgb">{row.rgb}</span>
		<span class="hsl">{row.hsl}</span>
	</div>
</FilterableList>
```

最后，移除不再需要的占位变量：

```svelte
/// file: App.svelte
<script>
	import FilterableList from './FilterableList.svelte';
	import { colors } from './colors.js';

	---let row = colors[0];---
</script>
```

> 命名槽也可以有属性（props）：在拥有 `slot="..."` 属性（attribute）的元素上使用 `let` 标志，而非直接在组件上用。
