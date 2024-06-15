---
title: 渐进增强
---

因为我们使用的是 `<form>`，我们的应用可以在用户没有 JavaScript 的时候依然有效，[这种情况可能比想象中要更常见](https://kryogenix.org/code/browser/everyonehasjs.html)。这挺好，因为这代表我们的应用是有弹性的。

但大部分时候，用户还是 _有_ JavaScript 的。在这种情况下，我们可以 _逐步增强_ 用户体验，就像 SvelteKit 使用客户端路由增强 `<a>` 元素一样。

从 `$app/forms` 导入 `enhance` 函数……

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { enhance } from '$app/forms';+++

	export let data;
	export let form;
</script>
```

……然后给 `<form>` 元素添加 `use:enhance` 标志：

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create" +++use:enhance+++>
```

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/delete" +++use:enhance+++>
```

然后就完事了！现在，当 JavaScript 可用时，`use:enhance` 会模仿浏览器原生的行为，而不是把整个页面重载，包括如下几件事：

- 更新 `form` 属性（prop）
- 成功响应后无效化所有数据，触发 `load` 函数重载（re-run）
- 通过重定向响应导航到新页面
- 如果发生错误则渲染最近的错误页面

既然我们现在是更新页面而非重载页面，我们可以使用比如过渡添加一些有意思的效果了：

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { fly, slide } from 'svelte/transition';+++
	import { enhance } from '$app/forms';

	export let data;
	export let form;
</script>
```

```svelte
/// file: src/routes/+page.svelte
<li +++in:fly={{ y: 20 }} out:slide+++>...</li>
```
