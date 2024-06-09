---
title: 添加参数
---

过渡函数可以接收参数，把 `fade` 过渡改为 `fly`……

```svelte
/// file: App.svelte
<script>
	import { +++fly+++ } from 'svelte/transition';
	let visible = true;
</script>
```

……然后把它加到 `p` 元素中并附加一些选项：

```svelte
/// file: App.svelte
<p transition:+++fly={{ y: 200, duration: 2000 }}+++>
	+++Flies+++ in and out
</p>
```

注意，过渡是 _可逆的_，这就意味着如果你在过渡期间切换了复选框，过渡会在当前位置转向，而不是在开始或者结束位置。
