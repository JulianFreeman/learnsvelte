---
title: page
---

我们在 [之前](writable-stores) 学过，Svelte 的存储（stores）是一个用来放置数据的、不属于任何一个组件的地方。

SvelteKit 通过 `$app/stores` 模块创建了三个只读存储：`page`、`navigating` 和 `updated`。其中最常用的就是 [`page`](https://kit.svelte.dev/docs/types#public-types-page)，用来提供有关当前页面的信息：

- `url` — 当前页面的 [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)
- `params` — 当前页面的 [参数](params)
- `route` — 一个拥有 `id` 属性（property）的代表当前路由的对象
- `status` — 当前页面的 HTTP 状态码
- `error` — 当前页面的错误对象，如果有的话（你会在 [之后的](error-basics) [练习](handleerror) 中学习更多关于错误处理的内容）
- `data` — 当前页面的数据，是所有 `load` 函数的集合
- `form` — 从 [表单操作](the-form-element) 中返回的数据

就跟其他的 store 一样，你可以在组件中通过在名称前添加 `$` 标志来引用其值。比如说，我们可以通过 `$page.url.pathname` 来获取当前路径：

```svelte
/// file: src/routes/+layout.svelte
+++<script>
	import { page } from '$app/stores';
</script>+++

<nav>
	<a href="/" +++aria-current={$page.url.pathname === '/'}+++>
		home
	</a>

	<a href="/about" +++aria-current={$page.url.pathname === '/about'}+++>
		about
	</a>
</nav>

<slot></slot>
```
