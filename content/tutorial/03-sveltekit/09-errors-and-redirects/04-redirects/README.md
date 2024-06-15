---
title: 重定向
---

我们也可以使用 `throw` 机制来从一个页面重定向另一个页面。

在 `src/routes/a/+page.server.js` 文件中创建一个新的 `load` 函数：

```js
/// file: src/routes/a/+page.server.js
import { redirect } from '@sveltejs/kit';

export function load() {
	throw redirect(307, '/b');
}
```

现在导航到 `/a` 会直接把我们带到 `/b`。

你可以在 `load` 函数、表单操作、API 路由和 `handle` 钩子函数（我们会在之后的章节中学习）中使用 `throw redirect(...)`。

你能用到的最常见的状态码：

- `303` — 用于表单操作，表示成功提交
- `307` — 用于临时重定向
- `308` — 用户永久重定向
