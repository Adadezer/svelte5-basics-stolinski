<script>
	import ChangeName from '$lib/components/ChangeName.svelte';

	let name = $state('Adadezer');
	let fake_name = 'Betinho';
</script>

<ChangeName {name} {fake_name} />

<button>teste classe global CSS (código comentado)</button>

<!-- :global() afeta o DOM inteiro (dentro e fora do componente).
       Estilos locais normalmente vencem o :global porque o Svelte
       adiciona uma classe de escopo, aumentando a ESPECIFICIDADE (especificidade é o numero de elementos, propriedades no seletor) deles.
       Se o seletor :global for mais específico (ou usar !important), ele vence. -->
<style>
	/* :global(button) {
		background-color: aqua;
	} */
</style>
