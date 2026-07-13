<script lang="ts">
	let { name }: { name: string } = $props();
</script>

<div class="header">
	<h1>Olá {name.replaceAll('d', 'D')}!</h1>
	<h2>do componente ChangeName</h2>
</div>
