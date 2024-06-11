---
title: 页面数据
path: /blog
---

SvelteKit 的核心工作可以归结为三件事：

1. **路由** — 处理访问的请求该匹配哪个路由的问题
2. **加载** — 获取页面需要的数据
3. **渲染** — （在服务端）生成 HTML，或者（在浏览器）更新 DOM

我们已经见过了路由和渲染，现在让我们聊聊中间的这一步——加载。

应用中的每一页都可以在 `+page.svelte` 文件同级下的 `+page.server.js` 文件中声明一个 `load` 函数。如同这个文件名所表示的，这个模块只在服务端运行，哪怕是处理客户端的导航。让我们添加一个 `src/routes/blog/+page.server.js` 文件，以用实际的博客页数据替换掉 `src/routes/blog/+page.svelte` 文件中的硬编码链接：

```js
/// file: src/routes/blog/+page.server.js
import { posts } from './data.js';

export function load() {
	return {
		summaries: posts.map((post) => ({
			slug: post.slug,
			title: post.title
		}))
	};
}
```

> 在本教程中，我们从 `src/routes/blog/data.js` 这个文件中导入的数据。在实际的应用中，你更可能会从数据库或者 CMS 中导入数据，但是目前，就先这样吧。

我们可以通过 `data` 属性在 `src/routes/blog/+page.svelte` 文件中获取这些数据：

```svelte
/// file: src/routes/blog/+page.svelte
+++<script>
	export let data;
</script>+++

<h1>blog</h1>

<ul>
---	<li><a href="/blog/one">one</a></li>
	<li><a href="/blog/two">two</a></li>
	<li><a href="/blog/three">three</a></li>---
+++	{#each data.summaries as { slug, title }}
		<li><a href="/blog/{slug}">{title}</a></li>
	{/each}+++
</ul>
```

然后，对于博客页也是同理：

```js
/// file: src/routes/blog/[slug]/+page.server.js
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	return {
		post
	};
}
```

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
+++<script>
	export let data;
</script>+++

---<h1>blog post</h1>---
+++<h1>{data.post.title}</h1>
<div>{@html data.post.content}</div>+++
```

还有最后一件事需要考虑，用户可能会访问一个不存在的路径，比如 `/blog/nope`，这种情况下我们需要回应一个 404 页面：

```js
/// file: src/routes/blog/[slug]/+page.server.js
+++import { error } from '@sveltejs/kit';+++
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	+++if (!post) throw error(404);+++

	return {
		post
	};
}
```

我们会在之后的章节中学习更多关于错误处理的内容。
