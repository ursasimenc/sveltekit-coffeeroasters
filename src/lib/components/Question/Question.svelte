<script lang="ts">
	import { slide } from "svelte/transition";
	export let open = false;
	export let disabled = false;
	function hideQuestion() {
		if (disabled) return;
		const svg = document.querySelector(`.svg-${id}`) as HTMLElement;
		svg.style.transform = open ? "rotate(0deg)" : "rotate(180deg)";
		open = !open;
	}
	export let h2 = "";
	export let id = "";
</script>

<fieldset class="group" disabled="{disabled ? true : false}" id="{id}">
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div class="label" on:click="{hideQuestion}" on:keydown="{hideQuestion}" aria-expanded="{open}">
		<legend>{h2}</legend>
		{#if !disabled}
			<div class="svg svg-{id}">
				<svg width="19" height="13" xmlns="http://www.w3.org/2000/svg"><path d="M15.949.586l2.828 2.828-9.096 9.096L.586 3.414 3.414.586l6.267 6.267z" fill="#0E8784" fill-rule="nonzero"></path></svg>
			</div>
		{/if}
	</div>
	{#if !disabled && open}
		<div class="question" transition:slide>
			<slot />
		</div>
	{/if}
</fieldset>

<style lang="scss">
	@import "$lib/styles/variables.scss";

	legend {
		color: $grey;

		@media (width >= $desktop) {
			@include h2();
		}

		@media ($tablet < width < $desktop) {
			@include h2(32px);
		}

		@media (width < $tablet) {
			@include h2(24px);
		}
	}

	.svg {
		@include flex();
		@include transition(transform);
	}

	.group {
		@include flex(start, start, column);
		@include size(100%, 100%);
		max-width: 725px;
		border: none;

		.label {
			@include flex(space-between, center);
			@include size(100%, auto);
			margin-bottom: 24px;
			cursor: pointer;
		}

		.question {
			@include transition(height);

			@media (width > $tablet) {
				@include size(100%, 250px);
				@include flex($gap: 24px);
			}

			@media (width < $tablet) {
				@include size(100%, auto);
				@include flex(center, center, column, 24px);
			}
		}
	}

	.group:disabled {
		opacity: 0.25;
	}
</style>
