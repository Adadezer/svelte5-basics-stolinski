<script lang="ts">
	let formState = $state({
		name: '',
		birthday: '',
		step: 0,
		error: ''
	});
</script>

<main>
	<p>Etapa: {formState.step + 1}</p>

	{#if formState.error}
		<p class="error">{formState.error}</p>
	{/if}

	{#if formState.step === 0}
		<div>
			<label for="name">Seu nome</label>
			<input type="text" id="name" bind:value={formState.name} />
		</div>
		<button
			onclick={() => {
				if (formState.name !== '') {
					formState.step++;
					formState.error = '';
				} else {
					formState.error = 'O campo nome está vazio. Por favor preencha seu nome';
				}
			}}>Next</button
		>
	{:else if formState.step === 1}
		<div>
			<label for="birthday">Data de nascimento</label>
			<input type="date" id="birthday" bind:value={formState.birthday} />
		</div>
		<button
			onclick={() => {
				if (formState.birthday !== '') {
					formState.step++;
					formState.error = '';
				} else {
					formState.error =
						'O campo data de nascimento está vazio. Por favor preencha sua data de nascimento';
				}
			}}>Next</button
		>
	{:else if formState.step === 2}
		<p>Nome: {formState.name}</p>
		<p>Data de nascimento: {formState.birthday.split('-').reverse().join('/')}</p>
	{/if}
</main>
