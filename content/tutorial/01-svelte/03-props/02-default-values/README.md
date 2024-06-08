---
title: 默认值
---

我们可以很容易地在 `Nested.svelte` 中设置属性的默认值：

```svelte
/// file: Nested.svelte
<script>
	export let answer +++= 'a mystery'+++;
</script>
```

如果我们现在添加第二个 _没有_ `answer` 属性的组件，就会显示默认值：

```svelte
/// file: App.svelte
<Nested answer={42}/>
+++<Nested />+++
```
