---
title: class 标志
---

就跟其他属性（attribute）一样，你可以将一个 JavaScript 属性（译注：可能是指 `script` 标签内的 JavaScript 变量）指定到 `class` 的值里。这里，我们可以给卡片添加一个 `flipped` 类。

```svelte
/// file: App.svelte
<button
	class="card +++{flipped ? 'flipped' : ''}+++"
	on:click={() => flipped = !flipped}
>
```

如期工作：如果你现在点击卡片，它就会翻转。

但我们可以做得更好。基于某些条件添加或者移除一个类，在 UI 开发中是一种十分常见的模式，因此 Svelte 提供了一个特殊的标志来简化流程：

```svelte
/// file: App.svelte
<button
	class="card"
	+++class:flipped={flipped}+++
	on:click={() => flipped = !flipped}
>
```

这个标志的意思是当 `flipped` 变量为真时，添加 `flipped` 类。