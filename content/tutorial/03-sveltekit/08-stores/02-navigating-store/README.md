---
title: navigating
---

`navigating` 这个 store 代表当前的导航。当导航触发时，不管是通过点击链接，或者一个前进/后退导航，或者程序控制的 `goto`，`navigating` 的值会变成一个拥有以下属性的对象：

- `from` 和 `to` — 拥有 `params`、`route` 和 `url` 属性（properties）的对象
- `type` — 导航的类型，比如 `link`，`popstate` 或者 `goto`

> 要了解完整的类型信息，阅读 [`Navigation`](https://kit.svelte.dev/docs/types#public-types-navigation) 文档。

我们也可以给一个需要花点时间的导航展示一个加载标志。在本例中，`src/routes/+page.server.js` 和 `src/routes/about/+page.server.js` 都有一个人工延迟。在 `src/routes/+layout.svelte` 文件中，导入 `navigating` 并向导航栏添加一条信息：

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, +++navigating+++ } from '$app/stores';
</script>

<nav>
	<a href="/" aria-current={$page.url.pathname === '/'}>
		home
	</a>

	<a href="/about" aria-current={$page.url.pathname === '/about'}>
		about
	</a>

+++	{#if $navigating}
		navigating to {$navigating.to.url.pathname}
	{/if}+++
</nav>

<slot></slot>
```
