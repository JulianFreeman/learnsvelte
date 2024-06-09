---
title: style 标志
---

就跟 `class` 一样，你也可以编写内联的 `style` 属性，因为 Svelte 真的就是 HTML 外加一点点改动：

```svelte
/// file: App.svelte
<button
	class="card"
	+++style="transform: {flipped ? 'rotateY(0)' : ''}; --bg-1: palegoldenrod; --bg-2: black; --bg-3: goldenrod"+++
	on:click={() => flipped = !flipped}
>
```

当你的样式越来越多的时候，看起来就有点乱了。我们可以使用 `style:` 标志来梳理一下：

```svelte
/// file: App.svelte
<button
	class="card"
+++	style:transform={flipped ? 'rotateY(0)' : ''}
	style:--bg-1="palegoldenrod"
	style:--bg-2="black"
	style:--bg-3="goldenrod"+++
	on:click={() => flipped = !flipped}
>
```