---
title: 第一个组件
---

在 Svelte 中，应用是由一个或多个 _组件_ 构成的。组件是一个可复用的自包含代码块，里面封装了一组相关的 HTML、CSS 和 JavaScript 代码，并写入一个 `.svelte` 文件。右侧代码编辑器中的 `App.svelte` 文件，就是一个简单的组件。

## 添加数据

一个只渲染静态标记（static markup）的组件没啥意思，让我们加点数据。

首先，向组件中添加一个 `script` 标签（tag），然后声明一个 `name` 变量：

```svelte
/// file: App.svelte
+++<script>
	let name = 'Svelte';
</script>+++

<h1>Hello world!</h1>
```

然后在标记（markup）中引用 `name`：

```svelte
/// file: App.svelte
<h1>Hello +++{name}+++!</h1>
```

任何 JavaScript 代码都可以放入花括号内。比如尝试把 `name` 改为 `name.toUpperCase()` 来打一个更有力量的招呼。

```svelte
/// file: App.svelte
<h1>Hello {name+++.toUpperCase()+++}!</h1>
```
