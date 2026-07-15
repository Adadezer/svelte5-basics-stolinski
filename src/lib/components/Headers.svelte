<script lang="ts">
	import { page } from '$app/state';

	// Mapa: caminho da URL -> nome do tópico.
	const TITLES: Record<string, string> = {
		'/state': 'State',
		'/derived': 'Derived',
		'/props': 'Props',
		'/logic': 'Lógica e Snippets',
		'/loop': 'Loops'
	};

	// page.url.pathname = caminho atual (ex.: '/loop'). $derived recalcula a cada navegação.
	let topic = $derived(TITLES[page.url.pathname] ?? '');
</script>

<div class="header">
	<button type="button" onclick={() => history.back()}>← Voltar</button>
	<h1>{topic ? `${topic} - ` : ''}Curso basico de Svelte 5</h1>
</div>

<style>
	.header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 0.75rem 1rem;
		background-color: #393837;
		color: #fa4b10;
	}

	button {
		padding: 0.5rem 0.75rem;
		border: 1px solid #ff5820;
		border-radius: 0.25rem;
		background: transparent;
		color: #ff5820;
		cursor: pointer;
	}
</style>
