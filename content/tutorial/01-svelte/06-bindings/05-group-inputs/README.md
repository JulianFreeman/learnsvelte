---
title: 组输入
---

如果你有多个关联到同一个值的 `type="radio"` 或者 `type="checkbox"`，你可以把 `bind:group` 跟 `value` 属性结合起来使用。同一个组内的单选框是互斥的，同一组内的复选框会组成一个选中值的数组。

给单选框添加 `bind:group={scoops}`……

```svelte
/// file: App.svelte
<input
	type="radio"
	name="scoops"
	value={number}
	+++bind:group={scoops}+++
/>
```

……然后给复选框添加 `bind:group={flavours}`：

```svelte
/// file: App.svelte
<input
	type="checkbox"
	name="flavours"
	value={flavour}
	+++bind:group={flavours}+++
/>
```
