<script>
	export let mode = "light";
</script>

<section class="how {mode}">
	{#if mode === "light"}
		<h4>How it works</h4>
	{/if}

	<div class="steps">
		<div class="step">
			<div class="bar">
				<div class="circle"></div>
				<div class="line"></div>
			</div>
			<div class="step-text">
				<h2>01</h2>
				<h4>Pick your coffee</h4>
				<p>Select from our evolving range of artisan coffees. Our beans are ethically sourced and we pay fair prices for them. There are new coffees in all profiles every month for you to try out.</p>
			</div>
		</div>
		<div class="step">
			<div class="bar">
				<div class="circle"></div>
				<div class="line"></div>
			</div>
			<div class="step-text">
				<h2>02</h2>
				<h4>Choose the frequency</h4>
				<p>Customize your order frequency, quantity, even your roast style and grind type. Pause, skip or cancel your subscription with no commitment through our online portal.</p>
			</div>
		</div>
		<div class="step">
			<div class="bar">
				<div class="circle"></div>
			</div>
			<div class="step-text">
				<h2>03</h2>
				<h4>Receive and enjoy!</h4>
				<p>We ship your package within 48 hours, freshly roasted. Sit back and enjoy award-winning world-class coffees curated to provide a distinct tasting experience.</p>
			</div>
		</div>
	</div>
	{#if mode === "light"}
		<a class="plan-button" href="/plan">Create your plan</a>
	{/if}
</section>

<style lang="scss">
	@import "$lib/styles/variables.scss";

	.how {
		@include size(100%, 100%);

		h2 {
			color: $paleOrange;
		}

		@media (width >= $desktop) {
			@include flex(center, start, column, 60px);
			& > h4 {
				@include h4();
				color: $grey;
			}
			.steps {
				@include flex(center, center, row, 0);
				@include size(100%, 100%);
				.step {
					@include flex(center, center, column, 60px);
					@include size(100%, 100%);

					.bar {
						@include size(100%, auto);
						@include flex(start);
						.circle {
							background-color: $bg;
							border: 1px solid $darkCyan;
							border-radius: 50%;
							@include size(31px);
							aspect-ratio: 1/1;
						}

						.line {
							background-color: $paleOrange;
							@include size(calc(100% - 31px), 1px);
						}
					}

					.step-text {
						@include flex(center, start, column, 32px);
						@include size(100%, 100%);

						h2 {
							@include h1();
						}

						h4 {
							@include h4();
						}

						p {
							@include p();
							@include size(300px, 130px);
						}
					}
				}
			}

			.plan-button {
				@include flex();
				@include button();
				text-decoration: none;
				color: $bg;
			}
		}
		@media ($tablet < width < $desktop) {
			@include flex(center, start, column, 60px);
			& > h4 {
				@include h4();
				color: $grey;
			}
			.steps {
				@include flex(center, start, row, 0);
				@include size(100%, 100%);

				.step {
					@include flex(center, start, column, 60px);
					@include size(100%, 100%);

					.bar {
						@include size(100%, auto);
						@include flex(start);
						.circle {
							background-color: $bg;
							border: 1px solid $darkCyan;
							border-radius: 50%;
							@include size(31px);
							aspect-ratio: 1/1;
						}

						.line {
							background-color: $paleOrange;
							@include size(calc(100% - 31px), 1px);
						}
					}

					.step-text {
						@include flex(start, start, column, 32px);
						@include size(80%, 100%);

						h2 {
							@include h1();
						}

						h4 {
							@include h4();
						}

						p {
							@include p();
						}
					}
				}
			}

			button {
				@include button();

				a {
					text-decoration: none;
					color: $bg;
				}
			}
		}
		@media (width < $tablet) {
			@include flex(center, center, column, 60px);

			& > h4 {
				@include h4();
				color: $grey;
			}
			.steps {
				@include flex(center, center, column, 60px);
				@include size(100%, 100%);

				.step {
					@include flex(center, center, column, 60px);
					@include size(100%, 100%);

					.bar {
						display: none;
					}

					.step-text {
						@include flex(start, center, column, 32px);
						@include size(85%, 100%);

						h2 {
							@include h1();
						}

						h4 {
							@include h4(24px);
						}

						p {
							@include p();
							text-align: center;
						}
					}
				}
			}

			button {
				@include button();

				a {
					text-decoration: none;
					color: $bg;
				}
			}
		}
	}

	.dark {
		color: $bg;
		background-color: $darkGreyBlue;
		background-size: cover;

		.steps {
			.step {
				.bar {
					.circle {
						background-color: transparent;
					}

					.line {
						background-color: $paleOrange;
					}
				}
			}
		}

		@media (width >= $desktop) {
			background-image: url("$lib/assets/plan/desktop/bg-steps.png");
			padding: 5rem;
		}

		@media ($tablet <width < $desktop) {
			background-image: url("$lib/assets/plan/tablet/bg-steps.png");
			@include size(100vw, 100%);
			padding: 2.5rem;
			border-radius: 8px;
		}

		@media (width < $tablet) {
			background-image: url("$lib/assets/plan/mobile/bg-steps.png");
			@include size(100vw, 100%);
			padding-block: 2.5rem;
			border-radius: 8px;
		}
	}

	.light {
		color: $darkGreyBlue;
	}
</style>
