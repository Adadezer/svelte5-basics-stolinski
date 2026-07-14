<script lang="ts">
	import type { Snippet } from 'svelte';

	let {
		name,
		children,
		secondChild
	}: { name?: string; children: Snippet; secondChild: Snippet<[string]> } = $props();
</script>

<div>
	<!-- Snippet children (implícito, passado para outro componente) -->
	{@render children()}

	<h1>
		{name ? name + ',' : ''} Este é o Formulário "Snippet"
	</h1>

	<!-- Snippet nomeado com argumento (secondChild) -->
	<h4>{@render secondChild('Iwazaki')}</h4>
</div>
