---
title: 添加参数
---

就跟过渡和动画一样，动作也可以有参数，参数会传递给动作函数，跟动作作用的元素一起调用。

在本例中，我们想使用 [`Tippy.js`](https://atomiks.github.io/tippyjs/) 库给 `button` 元素添加一个工具提示。我们已经添加这个动作了：`use:tooltip`，但是如果你把鼠标移动到按钮上方（或者使用键盘对焦），你会发现这个工具提示没有内容。

首先，这个动作需要接收一些选项，并把它们传递给 Tippy：

```js
/// file: App.svelte
function tooltip(node, +++options+++) {
	const tooltip = tippy(node, +++options+++);

	return {
		destroy() {
			tooltip.destroy();
		}
	};
}
```

然后我们需要传递一些选项到这个动作：

```svelte
/// file: App.svelte
<button use:tooltip+++={{ content, theme: 'material' }}+++>
	Hover me
</button>
```

现在这个工具提示几乎是可以工作了。但如果我们修改了 `input` 中的值，工具提示并不会展示新内容。我们可以通过给返回对象添加一个 `update` 方法来解决这点。

```js
/// file: App.svelte
function tooltip(node, options) {
	const tooltip = tippy(node, options);

	return {
+++		update(options) {
			tooltip.setProps(options);
		},+++
		destroy() {
			tooltip.destroy();
		}
	};
}
```
