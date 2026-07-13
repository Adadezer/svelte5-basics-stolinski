<script lang="ts">
	import Header from './Header.svelte';

	let name = $state('Adadezer');

	let status: 'ABERTA' | 'FECHADA' = $state('ABERTA');

	function toggle() {
		status = status === 'ABERTA' ? 'FECHADA' : 'ABERTA';
	}

	// Outra maneira de declarar função com true ou false
	let weekend = $state(false);

	function onclick() {
		weekend = !weekend;
	}

	let fullName = $derived(name + ' ' + 'Iwazaki');
</script>

<Header {name} />

<label for="name">Nome:</label>
<input id="name" type="text" bind:value={name} />

<div class="fullName">
	<h2>Nome e sobrenome:</h2>
	<h3>{fullName}</h3>
</div>

<p>Está loja agora está {status}</p>
<button onclick={toggle}>Toggle status</button>

<!-- shorthand, função e evento com o mesmo nome -->
<p>A loja abrirá nesse final de semana? {weekend ? 'Sim' : 'Não'}</p>
<button {onclick}>Toggle weekend</button>

<style>
	.fullName {
		display: flex;
		align-items: center;
		gap: 1rem;
	}
</style>
