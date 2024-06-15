---
title: $lib 别名
---

因为 SvelteKit 使用基于文件系统的路由，所以可以很容易地把页面会用到的模块和组件跟它们放在一起。一条好的经验法则是“就近原则”，也就是把代码放在靠近使用它们的地方。

有时候，代码可能会被很多地方使用。当遇到这种情况时，如果能有一个位置可以让所有页面都能获取到，而不用导入 `../../../../` 这样的前缀就好了。在 SvelteKit 中，这个位置就是 `src/lib` 目录。这个目录内的任何内容都可以被 `src` 中的任何模块以 `$lib` 别名获取。

本例中的两个 `+page.svelte` 文件都导入了 `src/lib/message.js`。但是如果你有一个嵌套很深的页面 `/a/deeply/nested/route`，应用就崩溃了，因为我们把前缀写错了。使用 `$lib/message.js` 更新：

```svelte
/// file: src/routes/a/deeply/nested/route/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>a deeply nested route</h1>
<p>{message}</p>
```

也同时更新 `src/routes/+page.svelte`：

```svelte
/// file: src/routes/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>home</h1>
<p>{message}</p>
```
