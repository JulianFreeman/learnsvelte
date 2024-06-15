---
title: 后备错误
---

如果事情变得十分糟糕，比如在加载根布局数据时出错，或者在渲染错误页面时出错，SvelteKit 会回退到一个静态的错误页面。

添加一个新的 `src/routes/+layout.server.js` 文件来观察效果：

```js
/// file: src/routes/+layout.server.js
export function load() {
	throw new Error('yikes');
}
```

你可以自定义这个备用的错误页面。创建 `src/error.html` 文件：

```html
/// file: src/error.html
<h1>Game over</h1>
<p>Code %sveltekit.status%</p>
<p>%sveltekit.error.message%</p>
```

这个文件可以包含如下信息：

- `%sveltekit.status%` — HTTP 状态码
- `%sveltekit.error.message%` — 错误信息
