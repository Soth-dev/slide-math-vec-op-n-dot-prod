<script lang="ts">
	import './layout.css';
	import favicon from '#lib/assets/favicon.svg';
	import type { LayoutProps } from './$types';

	let { children }: LayoutProps = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>
<h1>test</h1>
<body data-sveltekit-preload-data="hover" style="display: contents">
	{@render children()}
</body>

<style>
	body {
		height: 100%;
		margin: 0;
		background: var(--bg);
		color: var(--fg);
		font-family:
			system-ui,
			-apple-system,
			'Segoe UI',
			Roboto,
			sans-serif;
		overflow: hidden;
	}
</style>
