---
title: 路由参数
path: /blog
---

要根据动态参数创建路由，可以使用一个合法的变量名并用方括号包起来。比如说，一个形如 `src/routes/blog/[slug]/+page.svelte` 的文件，会匹配 `/blog/one`、`/blog/two`、`/blog/three` 等类似的路径并创建路由。

让我们来创建这个文件：

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
<h1>blog post</h1>
```

我们现在可以从 `/blog` 页面导航到单独的博客页了。在下一章，我们会学习如何加载内容。

> 一个 URL 段中可以出现多个路由参数，只要它们由至少一个静态字符分隔开就可以：`foo/[bar]x[baz]` 是一个合法的路由，其中 `[bar]` 和 `[baz]` 是动态参数。
