---
title: <svelte:element>
---

同样的，有时候我们并不能提前知道应该渲染什么样的 DOM 元素。这时候 `<svelte:element>` 就来救场了。就跟 [上一节](svelte-component) 一样，我们可以用一个动态的元素替换一系列的 `if` 块：

```svelte
/// file: App.svelte
<select bind:value={selected}>
	{#each options as option}
		<option value={option}>{option}</option>
	{/each}
</select>

+++<svelte:element this={selected}>
	I'm a <code>&lt;{selected}&gt;</code> element
</svelte:element>+++
```

`this` 的值可以是任意字符串，或者是一个假值，如果是假值，则不会渲染元素。