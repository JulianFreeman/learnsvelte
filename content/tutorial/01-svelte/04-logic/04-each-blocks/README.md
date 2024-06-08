---
title: Each 代码块
---

在构建用户界面的时候，你时常需要处理列表数据。在这个练习中，我们需要重复编写多个 `button` 标签，每次修改不同的颜色，但万一还有更多需要添加怎么办。

摒弃这种费力地拷贝、粘贴、修改，我们可以只用一个 `button` 外加一个 `each` 代码块：

```svelte
/// file: App.svelte
<div>
	+++{#each colors as color}+++
		<button
			aria-current={selected === 'red'}
			aria-label="red"
			style="background: red"
			on:click={() => selected = 'red'}
		></button>
	+++{/each}+++
</div>
```

> 表达式的部分（此例中的 `colors`）可以换成任何数组或者类似数组的对象（即有 `length` 属性）。你也可以直接用通用的可迭代对象：`each [...iterable]`。

现在我们需要用 `color` 变量替换掉 `"red"` ：

```svelte
/// file: App.svelte
<div>
	{#each colors as color}
		<button
			aria-current={selected === +++color+++}
			aria-label=+++{color}+++
			style="background: +++{color}+++"
			on:click={() => selected = +++color+++}
		></button>
	{/each}
</div>
```

你也可以通过第二个参数获取列表的当前 _索引_，比如：

```svelte
/// file: App.svelte
<div>
	{#each colors as color, +++i}+++
		<button
			aria-current={selected === color}
			aria-label={color}
			style="background: {color}"
			on:click={() => selected = color}
		>+++{i + 1}+++</button>
	{/each}
</div>
```
