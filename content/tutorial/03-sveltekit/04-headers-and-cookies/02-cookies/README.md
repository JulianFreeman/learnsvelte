---
title: 读写 cookies
---

上一节的 [`setHeaders`](headers) 函数无法使用 `Set-Cookie` 头，相反，你应该使用 `cookies` API。

在 `load` 函数内，你可以使用 `cookies.get(name, options)` 来读取 cookie：

```js
/// file: src/routes/+page.server.js
export function load(+++{ cookies }+++) {
	+++const visited = cookies.get('visited');+++

	return {
		visited: visited === 'true'
	};
}
```

要设置 cookie，使用 `cookies.set(name, value, options)`。我们强烈建议你在设置 cookie 的时候显式地设置 `path`，因为浏览器的默认行为是在当前路径的父路径上设置 cookie，尽管这看上去很没用。

```js
/// file: src/routes/+page.server.js
export function load({ cookies }) {
	const visited = cookies.get('visited');

	+++cookies.set('visited', 'true', { path: '/' });+++

	return {
		visited: visited === 'true'
	};
}
```

现在，如果你刷新教程窗口，`Hello stranger!` 会变成 `Hello friend!`。

调用 `cookies.set(name, ...)` 会触发更新 `Set-Cookie` 头，但这 _也_ 会更新 cookies 的内部映射，这意味着之后调用的 `cookies.get(name)` 会返回更新后的值。在底层实现中，`cookies` API 使用了著名的 `cookie` 包，传递到 `cookies.get` 和 `cookies.set` 的选项对应于 `cookie` [文档](https://github.com/jshttp/cookie#api) 的 `parse` 和 `serialize` 选项。SvelteKit 出于安全考虑给 cookies 设置了如下默认值：

```js
/// no-file
{
	httpOnly: true,
	secure: true,
	sameSite: 'lax'
}
```
