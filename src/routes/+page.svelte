<script>
	import Header from './Header.svelte';

	let name = $state('Iwazaki');
</script>

<Header {name} />

<label for="name">Nome:</label>
<input id="name" type="text" bind:value={name} />
