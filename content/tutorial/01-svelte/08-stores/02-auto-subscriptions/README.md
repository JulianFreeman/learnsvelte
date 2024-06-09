---
title: 自动订阅
---

上一节中的应用能用，但是有一个小小的 bug：那个 store 被订阅了，但是从没有取消订阅。如果这个组件会被创建和销毁好多次，那么就容易造成 _内存泄漏_。

在 `App.svelte` 中声明 `unsubscribe`：

```js
/// file: App.svelte
+++const unsubscribe =+++ count.subscribe((value) => {
	count_value = value;
});
```

> 调用 `subscribe` 方法会返回一个 `unsubscribe` 函数。

现在有 `unsubscribe` 了，但还需要调用，比如通过 `onDestroy` 这个生命周期函数来调用：

```svelte
/// file: App.svelte
<script>
	+++import { onDestroy } from 'svelte';+++
	import { count } from './stores.js';
	import Incrementer from './Incrementer.svelte';
	import Decrementer from './Decrementer.svelte';
	import Resetter from './Resetter.svelte';

	let count_value;

	const unsubscribe = count.subscribe(value => {
		count_value = value;
	});

	+++onDestroy(unsubscribe);+++
</script>

<h1>The count is {count_value}</h1>
```

事情开始变得麻烦起来，特别是你的组件需要订阅很多 store 的时候。这里，Svelte 有一个小妙招：你可以通过在 store 的名称前加 `$` 来引用 store 中的值：

```svelte
/// file: App.svelte
<script>
	---import { onDestroy } from 'svelte';---
	import { count } from './stores.js';
	import Incrementer from './Incrementer.svelte';
	import Decrementer from './Decrementer.svelte';
	import Resetter from './Resetter.svelte';

	---let count_value;---

	---const unsubscribe = count.subscribe(value => {
		count_value = value;
	});---

	---onDestroy(unsubscribe);---
</script>

<h1>The count is {+++$count+++}</h1>
```

> 自动订阅只对在一个组件最顶层范围上声明或导入的 store 变量有用。

对 `$count` 的使用不局限在标记代码（markup）中，你也可以在 `<script>` 标签内的任何地方使用，比如在事件处理器中或者响应式声明中。

> 任何以 `$` 开头的变量都会被默认当作一个 store 变量。因此这算是一个保留字符了，Svelte 会阻止你声明自己的带 `$` 前缀的变量。
