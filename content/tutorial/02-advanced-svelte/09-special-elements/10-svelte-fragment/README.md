---
title: <svelte:fragment>
---

`<svelte:fragment>` 元素允许你向一个命名槽中放置内容，而不必用 DOM 元素容器包裹。

在本例中，我们要编写一个 Tic-Tac-Toe 游戏。要绘制一个表格，`App.svelte` 中的 `button` 元素必须是 `Board.svelte` 中 `<div class="board">` 的直接后代。

但是现在，事情崩坏了。因为这些按钮实际是 `<div slot="game">` 的后代。让我们来修正它：

```svelte
/// file: App.svelte
<+++svelte:fragment+++ slot="game">
	{#each squares as square, i}
		<button
			class="square"
			class:winning={winningLine?.includes(i)}
			disabled={square}
			on:click={() => {
				squares[i] = next;
				next = next === 'x' ? 'o' : 'x';
			}}
		>
			{square}
		</button>
	{/each}
</+++svelte:fragment+++>
```