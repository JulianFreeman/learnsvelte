---
title: 槽
---

就跟元素可以包含子元素一样……

```html
/// no-file
<div>
	<p>I'm a child of the div</p>
</div>
```

……组件也可以包含子组件。在给组件添加子组件之前，它需要知道要把这个子组件放在什么位置。我们通过 `slot` 元素实现这点，把它加入到 `Card.svelte` 中：

```svelte
/// file: Card.svelte
<div class="card">
	+++<slot></slot>+++
</div>
```

现在你就可以给卡片添加内容了：

```svelte
/// file: App.svelte
<Card>
	+++<span>Patrick BATEMAN</span>+++
	+++<span>Vice President</span>+++
</Card>
```
