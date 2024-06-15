---
title: 错误页面
---

当 `load` 函数内出现错误时，SvelteKit 会渲染一个错误页面。

默认的错误页面有点索然无味，我们可以创建一个 `src/routes/+error.svelte` 组件来自定义：

```svelte
/// file: src/routes/+error.svelte
<script>
	import { page } from '$app/stores';
	import { emojis } from './emojis.js';
</script>

<h1>{$page.status} {$page.error.message}</h1>
<span style="font-size: 10em">
	{emojis[$page.status] ?? emojis[500]}
</span>
```

注意 `+error.svelte` 组件是在根组件 `+layout.svelte` 中渲染的。我们可以创建更细粒度的 `+error.svelte` 组件：

```svelte
/// file: src/routes/expected/+error.svelte
<h1>this error was expected</h1>
```

这个组件会在 `/expected` 下渲染，而根目录下的 `src/routes/+error.svelte` 页面会在任意其他错误出现时渲染。
