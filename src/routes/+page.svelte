<script>
	import granEspresso from "$lib/assets/home/desktop/image-gran-espresso.png";
	import planalto from "$lib/assets/home/desktop/image-planalto.png";
	import piccollo from "$lib/assets/home/desktop/image-piccollo.png";
	import danche from "$lib/assets/home/desktop/image-danche.png";
</script>

<main>
	<section class="hero">
		<div>
			<h1>Great coffee made simple.</h1>
			<p>Start your mornings with the world’s best coffees. Try our expertly curated artisan coffees from our best roasters delivered directly to your door, at your schedule.</p>
			<button><a href="/plan">Create your plan</a></button>
		</div>
	</section>
	<section class="collection">
		<h2 class="title">our collection</h2>
		<div class="collection-div">
			<div class="coffee">
				<img src="{granEspresso}" alt="Gran Espresso" />
				<div class="collection-text">
					<h4>Gran Espresso</h4>
					<p>Light and flavorful blend with cocoa and black pepper for an intense experience.</p>
				</div>
			</div>
			<div class="coffee">
				<img src="{planalto}" alt="Planalto" />
				<div class="collection-text">
					<h4>Planalto</h4>
					<p>Brazilian dark roast with rich and velvety body, and hints of fruits and nuts.</p>
				</div>
			</div>
			<div class="coffee">
				<img src="{piccollo}" alt="Piccollo" />
				<div class="collection-text">
					<h4>Piccollo</h4>
					<p>Mild and smooth blend featuring notes of toasted almond and dried cherry.</p>
				</div>
			</div>
			<div class="coffee">
				<img src="{danche}" alt="Danche" />
				<div class="collection-text">
					<h4>Danche</h4>
					<p>Ethiopian hand-harvested blend densely packed with vibrant fruit notes.</p>
				</div>
			</div>
		</div>
	</section>
</main>

<style lang="scss">
	@import "$lib/styles/variables.scss";

	main {
		@include size(100%, fit-content);
		@include flex(center, center, column, 200px);
		max-width: 1280px;

		@media ($tablet < width < $desktop) {
			gap: 100px;
		}

		@media (width < $tablet) {
			gap: 40px;
		}
	}

	.hero {
		@include size(100%, 600px);
		border-radius: 10px;

		div {
			@include size(100%, 100%);

			button {
				@include button();

				a {
					text-decoration: none;
					color: $bg;
				}
			}
		}

		@media (width >= $desktop) {
			background-image: url("$lib/assets/home/desktop/image-hero-coffeepress.jpg");
			background: contain no-repeat;
			background-position: right;
			div {
				@include flex(center, start, column, 32px);
				padding-left: 79px;
				h1 {
					@include h1();
					max-width: 500px;
				}

				p {
					@include p();
					max-width: 400px;
				}
			}
		}

		@media ($tablet < width < $desktop) {
			@include size(100%, 500px);
			background-image: url("$lib/assets/home/tablet/image-hero-coffeepress.jpg");
			background: cover;
			background-position: top right;
			div {
				@include flex(center, start, column, 32px);
				padding-left: 79px;

				h1 {
					@include h1(48px, 48px);
					max-width: 400px;
				}

				p {
					@include p(15px);
					max-width: 400px;
				}
			}
		}

		@media (width < $tablet) {
			@include size(100%, 500px);
			background-image: url("$lib/assets/home/mobile/image-hero-coffeepress.jpg");
			background: cover;
			background-position: top right;
			div {
				@include flex(center, center, column, 32px);
				padding: 1rem;

				h1 {
					@include h1(40px, 40px);
					max-width: 400px;
					text-align: center;
				}

				p {
					@include p(15px);
					max-width: 400px;
					text-align: center;
				}
			}
		}
	}

	.collection {
		color: $darkGreyBlue;
		margin: 1.5rem;
		@include size(100%, fit-content);
		@include flex(end, center, column);
		h2 {
			text-align: center;
			z-index: -1;
			position: relative;
		}

		@media (width >= $desktop) {
			img {
				@include size(256px, auto);
			}
			h2 {
				@include title(150px, 72px);
				@include size(100%, fit-content);
			}

			div {
				@include flex($gap: 2.5rem);
				@include size(100%, fit-content);

				.coffee {
					@include flex(end, center, column, 40px);

					.collection-text {
						@include flex(end, center, column, 24px);

						h4 {
							@include h4();
						}

						p {
							@include p();
							text-align: center;
						}
					}
				}
			}
		}

		@media ($tablet < width < $desktop) {
			img {
				@include size(155px, auto);
			}
			h2 {
				@include title(74px, 32px);
				@include size(100%, fit-content);
			}

			div {
				@include flex($gap: 1rem);
				@include size(100%, fit-content);

				.coffee {
					@include flex(end, center, column, 40px);

					.collection-text {
						@include flex(end, center, column, 24px);

						h4 {
							@include h4(22px, 22px);
							@include size(17.5vw, 45px);
							@include flex();
							text-align: center;
						}

						p {
							@include size(17.5vw, 110px);
							@include p(12px);
							text-align: center;
						}
					}
				}
			}
		}

		@media (width < $tablet) {
			gap: 2.5rem;
			img {
				@include size(200px, auto);
			}
			h2 {
				@include title(40px, 48px);
				@include size(100%, fit-content);
			}

			div {
				@include flex($gap: 2.5rem, $direction: column);
				@include size(100%, fit-content);

				.coffee {
					@include flex(end, center, column, 40px);

					.collection-text {
						@include flex(end, center, column, 24px);

						h4 {
							@include h4(22px, 22px);
							text-align: center;
						}

						p {
							@include size(80%, auto);
							@include p(15px);
							text-align: center;
						}
					}
				}
			}
		}
	}
</style>
