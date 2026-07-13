<script lang="ts">
	let { name }: { name: string } = $props();
</script>

<h1>Hello {name}, from Header</h1>
<h2>{name.replaceAll('d', 'D')}</h2>
