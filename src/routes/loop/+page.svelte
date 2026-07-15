<script lang="ts">
	import HeaderLoop from './HeaderLoop.svelte';

	const QUESTIONS = [
		{
			question: 'Qual é o seu nome?',
			id: 'name',
			type: 'text'
		},
		{
			question: 'Qual é a data do seu aniversário?',
			id: 'birthday',
			type: 'date'
		},
		{ question: 'Qual sua cor favorita?', id: 'color', type: 'color' }
	] as const; // `as const` marca o array como imutável e mantém os tipos LITERAIS.
	// Sem ele, o TS alarga `id: 'name'` para `id: string`.
	// Com `as const`, `id` continua sendo exatamente 'name' | 'birthday' | 'color'.

	// Extrai, a partir do array, a união dos ids possíveis: 'name' | 'birthday' | 'color'.
	// (typeof QUESTIONS)[number] = "um item qualquer do array"; ['id'] = pega a chave id desse item.
	type QuestionId = (typeof QUESTIONS)[number]['id'];

	let formState = $state({
		// `answers` é um "saco" de respostas indexado pelo id da pergunta.
		// Ex.: { name: 'Ada', birthday: '1990-01-01' }
		answers: {} as Record<QuestionId, string>,
		step: 0,
		error: ''
	});
</script>

<main class="container">
	<HeaderLoop name={formState.answers.name} />

	<p>Etapa: {formState.step + 1}</p>

	<!-- `(id)` é a chave (key) do #each: identifica cada item de forma única.
	     O Svelte passa a rastrear os itens pela identidade (o id), e não pela posição — assim, ao reordenar/remover, ele preserva o elemento e o
	     estado correto de cada item. Assim como o key em React -->
	{#each QUESTIONS as { id, question, type } (id)}
		{@render formStep({ question, id, type })}
	{/each}

	{#if formState.error}
		<p class="error">{formState.error}</p>
	{/if}

	<!-- `id` é tipado como QuestionId ('name' | 'birthday'), então bind:value só aceita
	     indexar formState.answers com uma chave que realmente existe. -->
	{#snippet formStep({ question, id, type }: { type: string; question: string; id: QuestionId })}
		<article>
			<div>
				<label for={id}>{question}</label>
				<input {type} {id} bind:value={formState.answers[id]} />
			</div>
		</article>
	{/snippet}
</main>

<style>
	.error {
		color: red;
	}
</style>
