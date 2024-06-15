---
title: 设置 headers
---

在 `load` 函数中（在 [表单操作](the-form-element)、[hooks](handle) 和 [API 路由](get-handlers) 中也同理，我们之后会学到），你可以使用一个 `setHeaders` 函数，来允许你给响应设置标头（headers）。

大部分时候，你会在其中用 [`Cache-Control`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) 响应头来自定义缓存行为。但是对于本教程而言，让我们做点不是那么推荐但很有意思的事情：

```js
/// file: src/routes/+page.server.js
export function load(+++{ setHeaders }+++) {
+++	setHeaders({
		'Content-Type': 'text/plain'
	});+++
}
```

（你可能需要刷新教程的渲染窗口才能看到效果。）
