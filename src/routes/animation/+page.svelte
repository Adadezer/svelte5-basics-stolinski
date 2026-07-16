<script lang="ts">
	import { fly } from 'svelte/transition';
	import HeaderAnimation from './HeaderAnimation.svelte';

	const QUESTIONS = [
		{
			question: 'Digite seu nome: ',
			id: 'name',
			type: 'text',
			field: 'nome'
		},
		{
			question: 'Informe sua data de nascimento: ',
			id: 'birthday',
			type: 'date',
			field: 'aniversário'
		},
		{ question: 'Escolha uma cor: ', id: 'color', type: 'color', field: 'cor' }
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

	function nextStep(id: QuestionId, field: string) {
		if (formState.answers[id]) {
			formState.step++;
			formState.error = '';
		} else {
			formState.error = `O campo ${field} está vazio. Por favor preencha este campo`;
		}
	}

	// `$inspect` é uma runa de depuração e funciona como um log, porém será atualizada sempre que um valor reativo for atualizado
	$inspect(formState.step);
</script>

<main class="container">
	<HeaderAnimation name={formState.answers.name} />

	{#if formState.step === QUESTIONS.length}
		<p>Obrigado!</p>
	{:else}
		<p>Step: {formState.step + 1}</p>
	{/if}

	<!-- - { id, question, type, field }: desestrutura os items do array QUESTIONS para obter as propriedades que eu quero.

      - `(id)` é a chave (key) do #each: identifica cada item de forma única. Assim como o key em React, que pede um id.
        O Svelte passa a rastrear os itens pela identidade (o id), e não pela posição — assim, ao reordenar/remover, ele preserva o elemento e o
        estado correto de cada item.
  -->
	{#each QUESTIONS as { id, question, type, field }, index (id)}
		{#if formState.step === index}
			<div
				in:fly={{ x: 300, duration: 300, opacity: 0, delay: 500 }}
				out:fly={{ x: -300, duration: 300, opacity: 0 }}
			>
				{@render formStep({ question, id, type, field })}
			</div>
		{/if}
	{/each}

	{#if formState.error}
		<p class="error">{formState.error}</p>
	{/if}

	<!-- `id` é tipado como QuestionId ('name' | 'birthday'), então bind:value só aceita
	     indexar formState.answers com uma chave que realmente existe. -->
	{#snippet formStep({
		question,
		id,
		type,
		field
	}: {
		type: string;
		question: string;
		id: QuestionId;
		field: string;
	})}
		<article>
			<div>
				<label for={id}>{question}</label>
				<input {type} {id} bind:value={formState.answers[id]} />
			</div>
			<button onclick={() => nextStep(id, field)}>Proxima</button>
		</article>
	{/snippet}
</main>

<style>
	.error {
		color: red;
	}
</style>
