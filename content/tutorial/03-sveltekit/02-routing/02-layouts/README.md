---
title: 布局
---

网页应用的不同页面往往会使用相同的 UI。为了避免在每一个 `+page.svelte` 组件中重复相同的内容，我们可以使用一个 `+layout.svelte` 组件来对同一目录内的所有页面应用相同的内容。

在本应用中我们有两个页面，`src/routes/+page.svelte` 和 `src/routes/about/+page.svelte`，两个页面有相同的导航 UI。让我们创建一个新文件 `src/routes/+layout.svelte`……

```
src/routes/
├ about/
│ └ +page.svelte
+++├ +layout.svelte+++
└ +page.svelte
```

……然后把 `+page.svelte` 文件中的相同内容转移到 `+layout.svelte` 文件。`<slot></slot>` 元素是页面内容进行渲染的位置：

```svelte
/// file: src/routes/+layout.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<slot></slot>
```

一个 `+layout.svelte` 文件会应用到所有的子页面中，也包括同级目录下的 `+page.svelte` （如果存在的话）。你可以将布局嵌入到任意深度。
