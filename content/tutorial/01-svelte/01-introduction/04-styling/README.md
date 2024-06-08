---
title: 添加样式
---

就像在 HTML 中一样，你也可以给组件添加 `style` 标签。让我们给 `p` 元素添加一些样式：

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>

<style>
+++	p {
		color: goldenrod;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}+++
</style>
```

值得注意的是，这些样式规则只在 _当前组件内_ 适用。因此你不用担心这些规则会一不小心影响到其他组件的 `p` 元素，这一点在之后的教程中会提到。
