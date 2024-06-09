---
title: 槽的默认内容
---

组件可以给任意留空的槽指定 _默认内容_，只需要将其放入 `slot` 元素内即可：

```svelte
/// file: Card.svelte
<div class="card">
	<header>
		<slot name="telephone">
			+++<i>(telephone)</i>+++
		</slot>
		
		<slot name="company">
			+++<i>(company name)</i>+++
		</slot>
	</header>

	<slot>
		+++<i>(name)</i>+++
	</slot>
		
	<footer>
		<slot name="address">
			+++<i>(address)</i>+++
		</slot>
	</footer>
</div>
```