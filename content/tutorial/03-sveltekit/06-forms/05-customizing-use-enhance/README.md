---
title: 自定义 use:enhance
---

有了 `use:enhance`，我们能做到的不只是模拟浏览器的原生行为。通过提供一个回调函数，我们可以实现如 **待定状态** 和 **乐观 UI** 的功能。让我们给两个操作添加一个人工延迟，来模拟网速慢的情况：

```js
/// file: src/routes/+page.server.js
export const actions = {
	create: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	},

	delete: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	}
};
```

当我们创建或者删除代办项的时候，会花费整整一秒才更新 UI，在这期间用户完全不知道发生了什么。要优化这点，让我们添加一些本地状态……

```svelte
/// file: src/routes/+page.svelte
<script>
	import { fly, slide } from 'svelte/transition';
	import { enhance } from '$app/forms';

	export let data;
	export let form;

+++	let creating = false;
	let deleting = [];+++
</script>
```

……然后在第一个 `use:enhance` 中切换 `creating`：

```svelte
/// file: src/routes/+page.svelte
<form
	method="POST"
	action="?/create"
+++	use:enhance={() => {
		creating = true;

		return async ({ update }) => {
			await update();
			creating = false;
		};
	}}+++
>
	<label>
		add a todo:
		<input
			+++disabled={creating}+++
			name="description"
			value={form?.description ?? ''}
			autocomplete="off"
			required
		/>
	</label>
</form>
```

现在我们在保存数据的同时就可以展示一个信息了：

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	<!-- ... -->
</ul>

+++{#if creating}
	<span class="saving">saving...</span>
{/if}+++
```

对于删除的情况，我们实际上不需要服务端验证什么，所以可以立即更新 UI：

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each +++data.todos.filter((todo) => !deleting.includes(todo.id))+++ as todo (todo.id)}
		<li in:fly={{ y: 20 }} out:slide>
			<form
				method="POST"
				action="?/delete"
				+++use:enhance={() => {
					deleting = [...deleting, todo.id];
					return async ({ update }) => {
						await update();
						deleting = deleting.filter((id) => id !== todo.id);
					};
				}}+++
			>
				<input type="hidden" name="id" value={todo.id} />
				<button aria-label="Mark as complete">✔</button>

				{todo.description}
			</form>
		</li>
	{/each}
</ul>
```

> `use:enhance` 是高度可定制的，你可以用 `cancel()` 取消提交，可以处理重定向，控制表单是否重置，等等。查看 [文档](https://kit.svelte.dev/docs/modules#$app-forms-enhance) 了解更多细节。
