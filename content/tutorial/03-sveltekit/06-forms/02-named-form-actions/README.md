---
title: 命名的表单操作
---

只有一个操作的页面在实际项目中极为少见，大部分时候，你需要在一个页面上进行多种操作。在本应用中，单是创建代办还不够，我们还想让它们在完成后被删除掉。

让我们把 `default` 操作替换为命名的 `create` 和 `delete` 操作：

```js
/// file: src/routes/+page.server.js
export const actions = {
	+++create+++: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}+++,+++

+++	delete: async ({ cookies, request }) => {
		const data = await request.formData();
		db.deleteTodo(cookies.get('userid'), data.get('id'));
	}+++
};
```

> 默认操作无法与命名操作共存。

`<form>` 元素有一个可选的 `action` 属性，就跟 `<a>` 元素的 `href` 属性差不多。更新表单以使其指向新创建的 `create` 操作：

```svelte
/// file: src/routes/+page.svelte
<form method="POST" +++action="?/create"+++>
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>
```

> `action` 属性可以是任意 URL，如果操作是在其他页面定义的，你可以使用形如 `/todos?/create` 的路径。因为我们的操作是定义在 _当前_ 页面上的，我们可以省略路径，直接以 `?` 字符开头。

接下来，我们想为每一个代办创建一个表单，以一个隐藏的 `<input>` 来唯一定位：

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each data.todos as todo (todo.id)}
		<li>
+++			<form method="POST" action="?/delete">
				<input type="hidden" name="id" value={todo.id} />
				<span>{todo.description}</span>
				<button aria-label="Mark as complete"></button>
			</form>+++
		</li>
	{/each}
</ul>
```
