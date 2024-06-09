---
title: Each 代码块绑定
---

你甚至可以绑定到 `each` 代码块的属性。

```svelte
/// file: App.svelte
{#each todos as todo}
	<li class:done={todo.done}>
		<input
			type="checkbox"
			+++bind:+++checked={todo.done}
		/>

		<input
			type="text"
			placeholder="What needs to be done?"
			+++bind:+++value={todo.text}
		/>
	</li>
{/each}
```

> 注意，跟这些 `input` 元素交互的时候会修改数组内容，如果你希望数组不被更改，那应该使用事件处理器而非绑定。
