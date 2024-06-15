---
title: 基础
---

在 SvelteKit 中有两类错误：_预期的_ 错误和 _未预期的_ 错误。

预期错误是指通过 `@sveltejs/kit` 的帮助函数 [`error`](https://kit.svelte.dev/docs/modules#sveltejs-kit-error) 创建的错误，如同 `src/routes/expected/+page.server.js` 文件中的那样：

```js
/// file: src/routes/expected/+page.server.js
import { error } from '@sveltejs/kit';

export function load() {
	throw error(420, 'Enhance your calm');
}
```

其他的错误，比如 `src/routes/unexpected/+page.server.js` 文件中的这个，会被当作是未预期的：

```js
/// file: src/routes/unexpected/+page.server.js
export function load() {
	throw new Error('Kaboom!');
}
```

当你抛出一个预期错误的时候，你实际上在告诉 SvelteKit “不用担心，我知道我在做什么”。而相对的，未预期错误会被当作应用的一个 bug。当出现未预期的错误时，其错误信息和追溯栈会被记录到控制台。

> 在之后的章节中我们会学习如何使用 `handleError` 这个 hook 来自定义错误处理。

如果你点击应用中的链接，你会发现一个重要的不同：预期的错误会展示给用户，而未预期的错误会被重定向，然后给用户展示一个通用的“内部错误”信息和 500 状态码。这是因为这种错误信息可能包含敏感数据。
