<script lang="ts">
	import HeaderFormSnippet from './HeaderFormSnippet.svelte';

	let formState = $state({
		name: '',
		birthday: '',
		step: 0,
		error: ''
	});
</script>

<main class="container">
	<!-- Snippet children (implícito, passado para outro componente. O h3 é o children de HeaderFormSnippet) -->
	<HeaderFormSnippet name={formState.name}>
		<h3>Olá {formState.name}!</h3>

		<!-- Snippet nomeado com argumento (secondChild) -->
		{#snippet secondChild(sobrenome)}
			Sobrenome: {sobrenome}
		{/snippet}
	</HeaderFormSnippet>

	<p>Etapa: {formState.step + 1}</p>

	<!--  Snippet local (declarado e usado no mesmo arquivo) -->
	{@render formStep({ question: 'Qual é o seu nome', id: 'name', type: 'text' })}

	<!-- aqui o id é tipado com keyof, do tipo formState. O typescript entende que o id tem que ser um dos keys de formState (name, birthday, step, error) -->
	{#snippet formStep({
		question,
		id,
		type
	}: {
		type: string;
		question: string;
		id: keyof typeof formState;
	})}
		<article>
			<div>
				<label for={id}>{question}</label>
				<input {type} {id} bind:value={formState[id]} />
			</div>
		</article>
	{/snippet}
</main>
