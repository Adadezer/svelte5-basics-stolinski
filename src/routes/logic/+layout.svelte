<script lang="ts">
	let { children } = $props();
</script>

<div class="logic-scope">
	{@render children()}
</div>

<style>
	.logic-scope :global(.container) {
		background-color: #ff5820;
		max-width: fit-content;
		padding: 10px;
		border-radius: 10px;
		margin: 10px 0;
	}
</style>
