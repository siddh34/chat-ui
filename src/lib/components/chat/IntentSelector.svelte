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

	let selectedIntent = intents[0];
	let expanded = false;

	function selectIntent(intent: string) {
		selectedIntent = intent;
		listCollapse();
		dispatch("select", { intent });
	}

	function listExpand() {
		expanded = true;
	}

	function listCollapse() {
		expanded = false;
	}
</script>

<div class="intent-selector" on:mouseenter={listExpand} on:mouseleave={listCollapse}>
	<div class="intent-list" class:expanded>
		{#each intents as intent}
			<div class="intent-item" on:click={() => selectIntent(intent)}>
				{intent}
			</div>
		{/each}
	</div>
	<div class="intent-selected">
		{selectedIntent}
	</div>
</div>

<style>
	.intent-selector {
		position: relative;
		display: inline-block;
		width: 200px;
	}

	.intent-selected {
		cursor: pointer;
		padding: 8px;
		border-radius: 8px;
		transition: background-color 0.3s, border-color 0.3s; /* Added border-color transition */
		background: var(--selected-background);
		color: var(--selected-color);
		border: 1px solid white;
	}

	.intent-selected:focus, /* Added focus state */
    .intent-selected:hover {
		border-color: var(--selected-border-hover); /* Optional hover effect for border */
	}

	.intent-list {
		position: absolute;
		bottom: 100%; /* Place above the selected intent */
		left: 0;
		right: 0;
		display: none;
		flex-direction: column;
		gap: 8px;
		padding: 8px;
		background: #141c24;
		color: var(--list-color);
		border: 1px solid sky;
		border-radius: 8px;
		box-shadow: 2px 2px 4px rgba(255, 255, 255, 0.4);
		transition: max-height 0.3s ease-out, opacity 0.3s ease-out;
		max-height: 0;
		opacity: 0;
		overflow: hidden;
		z-index: 1;
	}

	.intent-list.expanded {
		display: flex;
		max-height: 350px;
		opacity: 1;
	}

	.intent-item {
		cursor: pointer;
		padding: 5px;
		border: 1px solid transparent;
		border-radius: 4px;
		transition: background-color 0.3s;
	}

	.intent-item:hover {
		background-color: var(--item-hover-background);
		border-color: var(--item-hover-border);
	}
</style>
