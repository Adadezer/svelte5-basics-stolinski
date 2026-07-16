<script lang="ts">
	let { name }: { name?: string } = $props();
</script>

<div>
	<h1>
		Formulário do {name ? name : 'Usuário'}
	</h1>
</div>
