---
title: POST 处理器
---

你也可以添加可更改数据的处理器，比如 `POST`。大部分情况下，你应该使用 [表单操作](the-form-element) 来实现这点，因为这样代码量更少，而且在没有 JavaScript 的时候依然有效，让应用更有弹性。

在 'add a todo' 的 `<input>` 中的 `keydown` 事件处理器中，我们可以向服务端发送一些数据：

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	on:keydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

+++		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});+++

		input.value = '';
	}}
/>
```

这里，我们使用用户 cookies 中的 `userid` 向 `/todo` API 路由发送一些 JSON 数据，然后接收响应中新创建的代办的 `id`。

要创建 `/todo` 路由，向 `src/routes/todo/+server.js` 文件添加一个 `POST` 处理器，然后调用 `src/lib/server/database.js` 中的 `createTodo`：

```js
/// file: src/routes/todo/+server.js
import { json } from '@sveltejs/kit';
import * as database from '$lib/server/database.js';

export async function POST({ request, cookies }) {
	const { description } = await request.json();

	const userid = cookies.get('userid');
	const { id } = await database.createTodo({ userid, description });

	return json({ id }, { status: 201 });
}
```

就像 `load` 函数和表单操作中一样，`request` 参数是一个标准的 [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) 对象；`await request.json()` 会返回我们从事件处理器中发送的数据。

我们以 [201 Created](https://http.dog/201) 状态和数据库中新创建的代办的 `id` 返回响应。在事件处理器中，我们可以以此更新页面：

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	on:keydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});

+++		const { id } = await response.json();

		data.todos = [...data.todos, {
			id,
			description
		}];+++

		input.value = '';
	}}
/>
```

> 你应该仅以通过重新加载页面能获得相同结果的方式更改 `data`。
