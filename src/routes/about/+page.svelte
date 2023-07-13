<script>
	import commitmentImg from "$lib/assets/about/desktop/image-commitment.jpg";
	import qualityImg from "$lib/assets/about/desktop/image-quality.jpg";
</script>

<main>
	<section class="hero">
		<h2>About Us</h2>
		<p>
			Coffeeroasters began its journey of exotic discovery in 1999, highlighting stories of coffee from around the world. We have since been dedicated to bring the perfect cup - from bean to brew - in
			every shipment.
		</p>
	</section>
	<section class="commitment">
		<div class="commitment-img"><img src="{commitmentImg}" alt="Barista making coffee" /></div>
		<div class="commitment-text">
			<h2>Our commitment</h2>
			<p>
				We’re built on a simple mission and a commitment to doing good along the way. We want to make it easy for you to discover and brew the world’s best coffee at home. It all starts at the source.
				To locate the specific lots we want to purchase, we travel nearly 60 days a year trying to understand the challenges and opportunities in each of these places. We collaborate with exceptional
				coffee growers and empower a global community of farmers through with well above fair-trade benchmarks. We also offer training, support farm community initiatives, and invest in coffee plant
				science. Curating only the finest blends, we roast each lot to highlight tasting profiles distinctive to their native growing region.
			</p>
		</div>
	</section>
	<section class="quality">
		<div class="quality-text">
			<h2>Uncompromising quality</h2>
			<p>
				Although we work with growers who pay close attention to all stages of harvest and processing, we employ, on our end, a rigorous quality control program to avoid over-roasting or baking the
				coffee dry. Every bag of coffee is tagged with a roast date and batch number. Our goal is to roast consistent, user-friendly coffee, so that brewing is easy and enjoyable.
			</p>
		</div>
		<div class="quality-img"><img src="{qualityImg}" alt="Cup of coffee" /></div>
	</section>
</main>

<style lang="scss">
	@import "$lib/styles/variables.scss";
	img {
		border-radius: 8px;
	}

	main {
		@include size(100%, fit-content);
		@include flex(center, center, column, 200px);
		max-width: 1280px;

		@media ($tablet < width < $desktop) {
			gap: 100px;
		}

		@media (width < $tablet) {
			gap: 120px;
		}
	}

	.hero {
		border-radius: 10px;

		@media (width >= $desktop) {
			@include size(100%, 450px);
			@include flex(center, start, column, 32px);
			background-image: url("$lib/assets/about/desktop/image-hero-whitecup.jpg");
			background: contain no-repeat;
			background-position: right;
			padding-left: 79px;

			h2 {
				@include h2();
				max-width: 500px;
			}

			p {
				@include p();
				max-width: 400px;
			}
		}

		@media ($tablet < width < $desktop) {
			@include flex(center, start, column, 32px);
			@include size(100%, 400px);
			background-image: url("$lib/assets/about/tablet/image-hero-whitecup.jpg");
			background: cover;
			background-position: center right;
			padding-left: 79px;

			h2 {
				@include h2(48px, 48px);
				max-width: 400px;
			}

			p {
				@include p(15px);
				max-width: 400px;
			}
		}

		@media (width < $tablet) {
			@include size(100%, 400px);
			@include flex(center, center, column, 32px);
			background-image: url("$lib/assets/about/mobile/image-hero-whitecup.jpg");
			background: cover;
			background-position: center right;
			padding: 1rem;

			h2 {
				@include h2(40px, 40px);
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

	.commitment {
		color: $darkGreyBlue;

		@media (width >= $desktop) {
			@include size(100%, 100%);
			@include flex($justify: space-between, $gap: 120px);
			padding-inline: 85px;

			img {
				@include size(445px, 520px);
			}

			.commitment-text {
				@include flex(start, start, column, 32px);

				h2 {
					@include h2();
				}

				p {
					@include p();
				}
			}
		}

		@media ($tablet < width < $desktop) {
			@include flex($justify: space-between, $gap: 2.5rem);
			img {
				content: url("$lib/assets/about/tablet/image-commitment.jpg");
			}

			.commitment-text {
				@include flex(start, start, column, 1rem);

				h2 {
					@include h2(32px);
				}

				p {
					@include p(14px);
				}
			}
		}

		@media (width < $tablet) {
			@include flex(center, center, column, 2.5rem);
			img {
				content: url("$lib/assets/about/mobile/image-commitment.jpg");
				@include size(100%, 100%);
			}

			.commitment-text {
				@include flex(start, center, column, 1rem);

				h2 {
					@include h2(32px);
				}

				p {
					@include p(14px);
					text-align: center;
				}
			}
		}
	}
</style>
