<script lang="ts">
	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();

	const intents = [
		"Presentation",
		"LinkedIn post",
		"Image generation",
		"Video Generation",
		"Generate Songs",
		"Professional email",
	];

	function selectIntent(intent: string) {
		dispatch("select", { intent });
	}
</script>

<div class="intent-selector">
	{#each intents as intent}
		<div class="intent-item" on:click={() => selectIntent(intent)}>
			{intent}
		</div>
	{/each}
</div>

<style>
	.intent-selector {
		display: flex;
		flex-direction: column;
		gap: 8px;
		padding: 8px;
		background: white;
		border: 1px solid #ccc;
		border-radius: 8px;
	}
	.intent-item {
		cursor: pointer;
		padding: 8px;
		border: 1px solid transparent;
		border-radius: 4px;
		transition: background-color 0.3s;
	}
	.intent-item:hover {
		background-color: #f0f0f0;
		border-color: #ddd;
	}
</style>
