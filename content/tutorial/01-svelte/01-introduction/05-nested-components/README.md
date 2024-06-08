---
title: 嵌套组件
---

要是把整个应用都放在一个组件中的话，挺不现实的。相反，我们可以从其他文件导入组件，然后在标记（markup）中使用它们。

在 `App.svelte` 文件开头添加 `script` 标签（tag），导入 `Nested.svelte` 文件……

```svelte
/// file: App.svelte
+++<script>
	import Nested from './Nested.svelte';
</script>+++
```

……然后使用 `<Nested />` 组件：

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>
+++<Nested />+++
```

注意，尽管 `Nested.svelte` 也有一个 `p` 元素，但是 `App.svelte` 中的样式并没有影响到它。

> 组件的名字永远都是大写字母开头，以此来区分 HTML 元素。
