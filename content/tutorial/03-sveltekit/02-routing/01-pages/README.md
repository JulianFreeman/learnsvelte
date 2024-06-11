---
title: 页面
---

SvelteKit 使用基于文件系统的路由，这就是说，网页应用中的 _路由_，或者说，当一个用户导航到一个特定的 URL 之后网页该呈现什么，是由代码库中的目录结构定义的。

应用中在 `src/routes` 之下的每一个 `+page.svelte` 文件都会创建一个页面。当前应用中，我们只有一个页面 `src/routes/+page.svelte`，映射到路径就是 `/`。如果我们导航到 `/about`，就会出现 404 错误。

让我们解决这个问题。添加第二个页面 `src/routes/about/+page.svelte`，把 `src/routes/+page.svelte` 文件中的内容拷贝出来，然后做如下修改：

```svelte
/// file: src/routes/about/+page.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<h1>+++about+++</h1>
<p>this is the +++about+++ page.</p>
```

现在我们就可以在 `/` 和 `/about` 之间导航了。

> 跟传统的多页应用不同，导航到或者导航回 `/about` 更新的是当前页面的内容，就跟单页应用一样。这让我们同时利用了两种模式的好处：快速的服务器渲染启动，和即时导航。（这种行为可以被 [配置](https://kit.svelte.dev/docs/page-options)。）
