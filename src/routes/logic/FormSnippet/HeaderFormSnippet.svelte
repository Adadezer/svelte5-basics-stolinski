<script lang="ts">
	import type { Snippet } from 'svelte';

	let { name, children }: { name?: string; children: Snippet } = $props();
</script>

<div>
	{@render children()}

	<h1>
		{name ? name + ',' : ''} Este é o Formulário "Snippet"
	</h1>
</div>
