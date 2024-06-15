---
title: <form> 元素
---

在 [加载数据](page-data) 的章节，我们见过了如何从服务器获取数据到浏览器。有时候你需要相反的操作，即把数据从浏览器发送给服务器，这就引出了 `<form>`，网页平台用来提交数据的方式。

让我们来搭建一个代办应用。我们有一个由 `src/lib/server/database.js` 文件配置的内存数据库，还有在 `src/routes/+page.server.js` 文件中使用 [`cookies`](https://kit.svelte.dev/docs/load#cookies) API 的 `load` 函数，这样我们就可以为每一个用户单独设置代办列表。但是我们还需要添加一个 `<form>` 来创建新的代办：

```svelte
/// file: src/routes/+page.svelte
<h1>todos</h1>

+++<form method="POST">
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>+++

<ul class="todos">
```

如果你在 `<input>` 中输入些什么然后回车，浏览器会向当前页面发送一个 POST 请求（因为表单设置了 `method="POST"` 属性）。但是这会引发一个错误，因为我们还没有在服务端创建相应的 _操作_ 来处理这个 POST 请求。让我们现在添加：

```js
/// file: src/routes/+page.server.js
import * as db from '$lib/server/database.js';

export function load({ cookies }) {
	// ...
}

+++export const actions = {
	default: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}
};+++
```

`request` 参数是一个标准的 [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) 对象；`await request.formData()` 返回一个 [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) 实例。

当我们回车之后，数据库就会更新，页面也会重新加载新的数据。

注意我们不必写任何 `fetch` 代码，数据会自动更新。而且因为我们使用的是 `<form>` 元素，这个应用即便在 JavaScript 被禁用或者无法使用时依然能正常工作。
