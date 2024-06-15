---
title: 其他处理器
---

同理，我们给其他 HTTP 方法添加处理器。要添加一个 `/todo/[id]` 路由，可以创建 `src/routes/todo/[id]/+server.js` 文件，添加 `PUT` 和 `DELETE` 处理器来使用 `src/lib/server/database.js` 文件中的 `toggleTodo` 和 `deleteTodo` 函数切换和移除代办：

```js
/// file: src/routes/todo/[id]/+server.js
import * as database from '$lib/server/database.js';

export async function PUT({ params, request, cookies }) {
	const { done } = await request.json();
	const userid = cookies.get('userid');

	await database.toggleTodo({ userid, id: params.id, done });
	return new Response(null, { status: 204 });
}

export async function DELETE({ params, cookies }) {
	const userid = cookies.get('userid');

	await database.deleteTodo({ userid, id: params.id });
	return new Response(null, { status: 204 });
}
```

因为我们不需要向浏览器返回任何实际数据，我们使用 [204 No Content](https://http.dog/204) 状态返回一个空 [响应](https://developer.mozilla.org/en-US/docs/Web/API/Response)。

现在我们可以在事件处理器中与此端点进行交互：

```svelte
/// file: src/routes/+page.svelte
<label>
	<input
		type="checkbox"
		checked={todo.done}
		on:change={async (e) => {
			const done = e.currentTarget.checked;

+++			await fetch(`/todo/${todo.id}`, {
				method: 'PUT',
				body: JSON.stringify({ done }),
				headers: {
					'Content-Type': 'application/json'
				}
			});+++
		}}
	/>
	<span>{todo.description}</span>
	<button
		aria-label="Mark as complete"
		on:click={async (e) => {
+++			await fetch(`/todo/${todo.id}`, {
				method: 'DELETE'
			});

			data.todos = data.todos.filter((t) => t !== todo);+++
		}}
	></button>
</label>
```
