---
title: <svelte:head>
---

`<svelte:head>` 元素允许你向 `<head>` 中插入元素。这对于像 `<title>` 和 `<meta>` 这样的标签很有用，对搜索引擎优化（SEO）很重要。

但是因为要在教程里展示这样的效果很困难，因此这里我们换作演示另一种效果：加载样式表。

```svelte
/// file: App.svelte
<script>
	const themes = ['margaritaville', 'retrowave', 'spaaaaace', 'halloween'];
	let selected = themes[0];
</script>

+++<svelte:head>
	<link rel="stylesheet" href="/stylesheets/{selected}.css" />
</svelte:head>+++

<h1>Welcome to my site!</h1>
```

> 在服务端渲染（SSR）模式，`<svelte:head>` 的内容会跟 HTML 的其他内容分开返回。
