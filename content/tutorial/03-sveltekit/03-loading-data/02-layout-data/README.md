---
title: 布局数据
path: /blog
---

如同 `+layout.svelte` 文件给每个子页面创建 UI 一样，`+layout.server.js` 文件会为每个子页面加载数据。

假设我们想在我们的博客页上加一个“更多博客”的侧边栏，我们 _可以_ 在 `src/routes/blog/[slug]/+page.server.js` 文件中从 `load` 函数返回 `summaries`，就像我们在 `src/routes/blog/+page.server.js` 文件中做的那样，但这就有点重复了。

相反，让我们把 `src/routes/blog/+page.server.js` 改名为 `src/routes/blog/+layout.server.js`。注意 `/blog` 路由依然是正常的，`data.summaries` 在该页面依然可用。

现在，在布局中为博客页添加一个侧边栏：

```svelte
/// file: src/routes/blog/[slug]/+layout.svelte
<script>
	export let data;
</script>

<div class="layout">
	<main>
		<slot></slot>
	</main>

+++	<aside>
		<h2>More posts</h2>
		<ul>
			{#each data.summaries as { slug, title }}
				<li>
					<a href="/blog/{slug}">{title}</a>
				</li>
			{/each}
		</ul>
	</aside>+++
</div>

<style>
	@media (min-width: 640px) {
		.layout {
			display: grid;
			gap: 2em;
			grid-template-columns: 1fr 16em;
		}
	}
</style>
```

布局页以及其下的所有页面都从其父文件 `+layout.server.js` 中继承了 `data.summaries`。

当我们从一个博客页导航到另一个博客页的时候，我们只需要加载目标博客页需要的内容，但布局数据依然有效。查看 [无效化](https://kit.svelte.dev/docs/load#rerunning-load-functions) 文档了解更新信息。
