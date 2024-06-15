---
title: updated
---

`updated` 这个 store 包含 `true` 或者 `false`，其值取决于页面在第一次打开后应用是否有新版本被部署。要实现这点，你的 `svelte.config.js` 文件必须指定 `kit.version.pollInterval`。

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, navigating, +++updated+++ } from '$app/stores';
</script>
```

版本变更只会在生产环境中发生，而不是开发环境。基于此，`$updated` 在本教程中会永远为 `false`。

你可以通过调用 `updated.check()` 手动检查新版本，而不用管 `pollInterval`。

```svelte
/// file: src/routes/+layout.svelte

+++{#if $updated}+++
	<div class="toast">
		<p>
			A new version of the app is available

			<button on:click={() => location.reload()}>
				reload the page
			</button>
		</p>
	</div>
+++{/if}+++
```
