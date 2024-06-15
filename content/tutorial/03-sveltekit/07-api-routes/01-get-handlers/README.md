---
title: GET 处理器
---

SvelteKit 不止可以用来创建页面，我们也可以创建 _API 路由_，只需要添加一个 `+server.js` 文件，然后导出跟 HTTP 方法对应的函数：`GET`、`PUT`、`POST`、`PATCH` 和 `DELETE`。

本应用会在你点击按钮时，从一个 `/roll` API 抓取数据。添加一个 `src/routes/roll/+server.js` 文件来创建路由：

```js
/// file: src/routes/roll/+server.js
export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});
}
```

现在点击按钮就可以正常工作了。

请求处理器必须返回一个 [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response/Response) 对象。因为从一个 API 路由返回 JSON 太常见了，SvelteKit 提供了一个便捷的函数来生成这样的响应对象：

```js
/// file: src/routes/roll/+server.js
+++import { json } from '@sveltejs/kit';+++

export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

---	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});---
+++	return json(number);+++
}
```
