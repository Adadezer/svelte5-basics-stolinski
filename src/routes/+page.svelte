<script lang="ts">
	import Header from './Header.svelte';

	let name = $state('Iwazaki');

	let status: 'ABERTA' | 'FECHADA' = $state('ABERTA');

	function toggle() {
		status = status === 'ABERTA' ? 'FECHADA' : 'ABERTA';
	}
</script>

<Header {name} />

<label for="name">Nome:</label>
<input id="name" type="text" bind:value={name} />

<p>Está loja agora está {status}</p>
<button onclick={toggle}>Toggle status</button>
