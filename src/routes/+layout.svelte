<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';

	import Headers from '$lib/components/Headers.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<Headers />

{@render children()}
