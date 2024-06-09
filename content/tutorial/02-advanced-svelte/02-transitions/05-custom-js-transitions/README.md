---
title: 自定义 JS 过渡
---

尽管大部分时候你都应该尽可能地使用 CSS 实现过渡，但有些效果没有 JavaScript 还真实现不了，比如打字机效果：

```js
/// file: App.svelte
function typewriter(node, { speed = 1 }) {
	const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

	if (!valid) {
		throw new Error(`This transition only works on elements with a single text node child`);
	}

	+++const text = node.textContent;
	const duration = text.length / (speed * 0.01);

	return {
		duration,
		tick: (t) => {
			const i = Math.trunc(text.length * t);
			node.textContent = text.slice(0, i);
		}
	};+++
}
```
