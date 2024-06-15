---
title: 验证
---

用户是一群调皮蛋，总会抓住一切机会提交各种没有意义的数据。为了避免他们引发混乱，我们需要对表单数据进行验证。

第一道防线是浏览器 [内置的表单验证](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation#using_built-in_form_validation)，比如说，可以让我们很容易地将一个 `<input>` 元素标记为必需：

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create">
	<label>
		add a todo
		<input
			name="description"
			autocomplete="off"
			+++required+++
		/>
	</label>
</form>
```

尝试在 `<input>` 留空时敲击回车。

这种验证很有效，但是还不够。有些验证规则（比如唯一性验证）无法通过 `<input>` 属性来实现。而且，如果用户是一个高级黑客，他完全可以使用浏览器的开发者工具把这个属性删掉。要防范这些恶作剧，你应该总是使用服务端验证。

在 `src/lib/server/database.js` 文件中，验证代办描述存在且唯一：

```js
/// file: src/lib/server/database.js
export function createTodo(userid, description) {
+++	if (description === '') {
		throw new Error('todo must have a description');
	}+++

	const todos = db.get(userid);

+++	if (todos.find((todo) => todo.description === description)) {
		throw new Error('todos must be unique');
	}+++

	todos.push({
		id: crypto.randomUUID(),
		description,
		done: false
	});
}
```

尝试提交一个重复的代办，呀，SvelteKit 抛出了一个不是很友好的错误页面。在服务端，我们看到了一个 'todos must be unique' 错误，但是 SvelteKit 在用户端隐藏了未预期的错误消息，因为这通常会包含一些敏感数据。

如果能在错误出现时停在同一页面并给出一个错误提示会更好，这样用户能知道问题出在哪并更正。要实现这点，我们可以使用 `fail` 函数来返回从操作来的数据，并附加一个合适的 HTTP 状态码：

```js
/// file: src/routes/+page.server.js
+++import { fail } from '@sveltejs/kit';+++
import * as db from '$lib/server/database.js';

export function load({ cookies }) {...}

export const actions = {
	create: async ({ cookies, request }) => {
		const data = await request.formData();

+++		try {+++
			db.createTodo(cookies.get('userid'), data.get('description'));
+++		} catch (error) {
			return fail(422, {
				description: data.get('description'),
				error: error.message
			});
		}+++
	}
```

在 `src/routes/+page.svelte` 文件中，我们可以通过 `form` 属性（prop）获取返回的值，这个属性只会在表单提交之后被赋值：

```svelte
/// file: src/routes/+page.svelte
<script>
	export let data;
	+++export let form;+++
</script>

<div class="centered">
	<h1>todos</h1>
	
	+++{#if form?.error}
		<p class="error">{form.error}</p>
	{/if}+++
	
	<form method="POST" action="?/create">
		<label>
			add a todo:
			<input
				name="description"
				+++value={form?.description ?? ''}+++
				autocomplete="off"
				required
			/>
		</label>
	</form>
```

> 你也可以从操作返回普通数据，而 _不用_ `fail` 函数封装，比如说当数据成功保存后显示一个“成功！”的信息，这个值也可以通过 `form` 属性获取。
