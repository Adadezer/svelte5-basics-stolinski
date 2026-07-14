<script lang="ts">
	let { name, fake_name }: { name: string; fake_name?: string } = $props();
</script>

<div class="header">
	<h1>Olá {name.replaceAll('d', 'D')}!</h1>
	<h2>do componente ChangeName</h2>

	<p>fake name?: {fake_name}</p>
</div>
