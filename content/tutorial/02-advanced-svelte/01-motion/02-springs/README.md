---
title: 弹簧
---

`spring` 函数作为 `tweened` 的替代，通常在面对经常变化的值时效果更好。

在本例中，有两个 store，其中一个表示圆圈的坐标，另一个表示圆圈的大小。让我们将其转换为 spring：

```svelte
/// file: App.svelte
<script>
	import { +++spring+++ } from 'svelte/+++motion+++';

	let coords = +++spring+++({ x: 50, y: 50 });
	let size = +++spring+++(10);
</script>
```

两个 spring 各有默认的 `stiffness` and `damping` 值，用来控制弹簧的……弹性。我们也可以手动指定初始值：

```js
/// file: App.svelte
let coords = spring({ x: 50, y: 50 }, +++{
	stiffness: 0.1,
	damping: 0.25
}+++);
```

晃动你的鼠标，尝试修改滑块的值来感受一下其对弹簧行为的影响。注意在弹簧仍在运动的期间，你依然可以修改这些值。
