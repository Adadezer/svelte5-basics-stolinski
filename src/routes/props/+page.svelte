<script>
	import ChangeName from '$lib/components/ChangeName.svelte';

	let name = $state('Adadezer');
	let fake_name = 'Betinho';
</script>

<ChangeName {name} {fake_name} />
