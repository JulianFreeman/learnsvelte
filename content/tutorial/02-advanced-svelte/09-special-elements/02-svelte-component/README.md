---
title: <svelte:component>
---

一个组件可以通过 `<svelte:component>` 完全变更其类型。在本例中，我们希望 `color` 为 `red` 的时候展示 `RedThing.svelte`，而为 `green` 的时候展示 `GreenThing.svelte`，以此类推。

我们 _可以_ 用一系列的 `if` 块来实现这个……

```svelte
/// file: App.svelte
{#if selected.color === 'red'}
	<RedThing/>
{:else if selected.color === 'green'}
	<GreenThing/>
{:else if selected.color === 'blue'}
	<BlueThing/>
{/if}
```

……但，这就有点繁琐。因此，我们可以创建一个动态的组件：

```svelte
/// file: App.svelte
<select bind:value={selected}>
	{#each options as option}
		<option value={option}>{option.color}</option>
	{/each}
</select>

+++<svelte:component this={selected.component} />+++
```

`this` 的值可以是任意组件构造器，或者是一个假值，如果是假值，就不渲染该组件。
