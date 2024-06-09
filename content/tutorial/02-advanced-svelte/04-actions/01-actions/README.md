---
title: use 标志
---

动作是一系列元素层级的生命周期函数，它们在以下场景中会很有用：

- 与第三方库进行接口对接
- 延迟加载图像
- 工具提示（tooltips）
- 添加自定义的事件处理器

在本例中，你可以在 `canvas` 上涂涂画画，通过菜单更换画笔颜色和大小。但是如果你打开菜单后使用 Tab 键在选项间切换，你会发现焦点并没有被窗口 _捕获_。

我们可以使用动作来解决这一点。从 `actions.js` 中导入 `trapFocus`……

```svelte
/// file: App.svelte
<script>
	import Canvas from './Canvas.svelte';
	+++import { trapFocus } from './actions.js';+++

	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet', 'white', 'black'];
	let selected = colors[0];
	let size = 10;

	let showMenu = true;
</script>
```

……然后使用 `use:` 标志将其添加到菜单中：

```svelte
/// file: App.svelte
<div class="menu" +++use:trapFocus+++>
```

让我们看一看 `actions.js` 中的这个 `trapFocus` 函数。一个动作函数接收一个 `node` 参数，也就是本例中的 `<div class="menu">`，当这个节点被初始化（mount）到 DOM 的时候，该动作函数被调用，然后返回一个包含 `destroy` 方法的动作对象。

首先，我们需要添加一个事件监听器来截获 Tab 按下事件：

```js
/// file: actions.js
focusable()[0]?.focus();

+++node.addEventListener('keydown', handleKeydown);+++
```

然后我们需要在节点被销毁时作一些清理工作：移除事件监听器，然后把焦点恢复到元素初始化之前的地方：

```js
/// file: actions.js
focusable()[0]?.focus();

node.addEventListener('keydown', handleKeydown);

+++return {
	destroy() {
		node.removeEventListener('keydown', handleKeydown);
		previous?.focus();
	}
};+++
```

现在，当你打开菜单的时候，就可以使用 Tab 键切换选项了。
