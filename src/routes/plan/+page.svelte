<script lang="ts">
	import Steps from "$lib/components/Steps/Steps.svelte";
	import Question from "$lib/components/Question/Question.svelte";

	export let open_coffee = true;
	export let open_beans = false;
	export let open_quantity = false;
	export let open_grind = false;
	export let open_frequency = false;

	export let plan = {
		coffee: "_____",
		beans: "_____",
		quantity: "_____",
		grind: "_____",
		frequency: "_____",
		price: 0,
	};
	let showModal = false;

	function setQuestion(value = "", name = "") {
		switch (name) {
			case "coffee":
				plan.coffee = value;
				if (plan.coffee === "capsule") {
					open_beans = false;
				}
				break;
			case "beans":
				plan.beans = value;
				break;
			case "quantity":
				plan.quantity = value;
				break;
			case "grind":
				plan.grind = value;
				break;
			case "frequency":
				plan.frequency = value;
				break;
		}
	}

	const makePlan = (e: Event) => {
		e.preventDefault();

		if (plan.coffee === "_____" || plan.beans === "_____" || plan.quantity === "_____" || plan.frequency === "_____") {
			alert("Please fill out all the fields");
			return;
		} else if (plan.coffee === "capsule" && plan.grind !== "_____") {
			alert("Please fill out all the fields");
			return;
		}

		switch (plan.frequency) {
			case "Every week":
				switch (plan.quantity) {
					case "250g":
						plan.price = 7.2;
						break;
					case "500g":
						plan.price = 13;
						break;
					case "1000g":
						plan.price = 22;
						break;
				}

				plan.price = plan.price * 4;
				break;
			case "Every 2 weeks":
				switch (plan.quantity) {
					case "250g":
						plan.price = 9.6;
						break;
					case "500g":
						plan.price = 17.5;
						break;
					case "1000g":
						plan.price = 32;
						break;
				}

				plan.price = plan.price * 2;
				break;
			case "Every month":
				switch (plan.quantity) {
					case "250g":
						plan.price = 12;
						break;
					case "500g":
						plan.price = 22;
						break;
					case "1000g":
						plan.price = 42;
						break;
				}
				break;
		}

		console.log(plan);

		showModal = true;
	};
</script>

<svelte:head>
	<title>Choose your plan</title>
</svelte:head>

<dialog style="{showModal ? '' : 'display: none;'}" open="{showModal}">
	<div class="popup">
		<div class="popup-header">Order Summary</div>
		<div class="popup-content">
			<div class="plan">
				“I drink my coffee {plan.coffee === "Capsules" ? "using" : "as"} <span>{plan.coffee}</span>, with a <span>{plan.beans}</span> type of bean.
				{#if plan.coffee === "Capsules"}
					Sent
				{:else}
					<span>{plan.quantity}</span> ground ala <span>{plan.grind}</span>, sent
				{/if}
				to me <span>{plan.frequency}</span>.”
			</div>
			<div class="confirmation">Is this correct? You can proceed to checkout or go back to plan selection if something is off. Subscription discount codes can also be redeemed at the checkout.</div>
		</div>
		<div class="popup-footer">
			<div class="price">${plan.price}/mo</div>
			<div>
				<button
					on:click="{() => {
						showModal = false;
					}}"
					on:keydown="{() => {
						showModal = false;
					}}">Checkout</button
				>
			</div>
		</div>
	</div>
</dialog>

<main>
	<section class="hero">
		<h2>Create plan</h2>
		<p>Coffee the way you wanted it to be. For coffee delivered tomorrow, or next week. For whatever brew method you use. For choice, for convenience, for quality.</p>
	</section>
	<Steps mode="dark" />
	<form on:submit="{(e) => makePlan(e)}">
		<div class="legend">
			<div
				on:click="{() => {
					open_coffee = !open_coffee;
				}}"
				on:keydown="{() => {
					open_coffee = !open_coffee;
				}}"
				aria-pressed="true"
				role="button"
				tabindex="0"
				class="{plan.coffee === '_____' ? 'undecided' : ''}"
			>
				<span>01</span> Preferences
			</div>

			<div class="line"></div>
			<div
				on:click="{() => {
					open_beans = !open_beans;
				}}"
				on:keydown="{() => {
					open_beans = !open_beans;
				}}"
				aria-pressed="true"
				role="button"
				tabindex="0"
				class="{plan.beans === '_____' ? 'undecided' : ''}"
			>
				<span>02</span> Bean Type
			</div>
			<div class="line"></div>
			<div
				on:click="{() => {
					open_quantity = !open_quantity;
				}}"
				on:keydown="{() => {
					open_quantity = !open_quantity;
				}}"
				aria-pressed="true"
				role="button"
				tabindex="0"
				class="{plan.quantity === '_____' ? 'undecided' : ''}"
			>
				<span>03</span> Quantity
			</div>
			<div class="line"></div>
			<div
				on:click="{() => {
					open_grind = !open_grind;
				}}"
				on:keydown="{() => {
					open_grind = !open_grind;
				}}"
				aria-pressed="true"
				role="button"
				tabindex="0"
				class="{plan.grind === '_____' ? 'undecided' : ''} {plan.coffee === 'Capsules' ? 'disabled' : ''}"
			>
				<span>04</span> Grind Option
			</div>
			<div class="line"></div>
			<div
				on:click="{() => {
					open_frequency = !open_frequency;
				}}"
				on:keydown="{() => {
					open_frequency = !open_frequency;
				}}"
				aria-pressed="true"
				role="button"
				tabindex="0"
				class="{plan.frequency === '_____' ? 'undecided' : ''}"
			>
				<span>05</span> Frequency
			</div>
		</div>
		<div class="content">
			<div class="questions">
				<Question h2="{'How do you drink your coffee?'}" id="coffee" open="{open_coffee}">
					<input type="radio" name="preference" id="capsule" on:change="{() => setQuestion('Capsules', 'coffee')}" checked="{plan.coffee === 'capsule' ? true : false}" />
					<input type="radio" name="preference" id="filter" on:change="{() => setQuestion('Filter', 'coffee')}" checked="{plan.coffee === 'filter' ? true : false}" />
					<input type="radio" name="preference" id="espresso" on:change="{() => setQuestion('Espresso', 'coffee')}" checked="{plan.coffee === 'espresso' ? true : false}" />
					<label for="capsule"
						><h4>Capsule</h4>
						<p>Compatible with Nespresso systems and similar brewers</p></label
					>
					<label for="filter"
						><h4>Filter</h4>
						<p>For pour over or drip methods like Aeropress, Chemex, and V60</p></label
					>
					<label for="espresso"
						><h4>Espresso</h4>
						<p>Dense and finely ground beans for an intense, flavorful experience</p></label
					>
				</Question>
				<Question h2="{'What type of coffee?'}" id="beans" open="{open_beans}">
					<input type="radio" name="bean-type" id="single-origin" on:change="{() => setQuestion('Single Origin', 'beans')}" checked="{plan.beans === 'Single Origin' ? true : false}" />
					<input type="radio" name="bean-type" id="decaf" on:change="{() => setQuestion('Decaf', 'beans')}" checked="{plan.beans === 'Decaf' ? true : false}" />
					<input type="radio" name="bean-type" id="blended" on:change="{() => setQuestion('Blended', 'beans')}" checked="{plan.beans === 'Blended' ? true : false}" />
					<label for="single-origin"
						><h4>Single Origin</h4>
						<p>Distinct, high quality coffee from a specific family-owned farm</p></label
					>
					<label for="decaf"
						><h4>Decaf</h4>
						<p>Just like regular coffee, except the caffeine has been removed</p></label
					>
					<label for="blended"
						><h4>Blended</h4>
						<p>Combination of two or three dark roasted beans of organic coffees</p></label
					>
				</Question>
				<Question h2="{'How much would you like?'}" id="quantity" open="{open_quantity}">
					<input type="radio" name="quantity" id="quarter" on:change="{() => setQuestion('250g', 'quantity')}" checked="{plan.quantity === '250g' ? true : false}" />
					<input type="radio" name="quantity" id="half" on:change="{() => setQuestion('500g', 'quantity')}" checked="{plan.quantity === '500g' ? true : false}" />
					<input type="radio" name="quantity" id="one" on:change="{() => setQuestion('1000g', 'quantity')}" checked="{plan.quantity === '1000g' ? true : false}" />
					<label for="quarter"
						><h4>250g</h4>
						<p>Perfect for the solo drinker. Yields about 12 delicious cups.</p>
					</label>
					<label for="half"
						><h4>500g</h4>
						<p>Perfect option for a couple. Yields about 40 delectable cups.</p>
					</label>
					<label for="one"
						><h4>1000g</h4>
						<p>Perfect for offices and events. Yields about 90 delightful cups.</p>
					</label>
				</Question>
				<Question h2="{'Want us to grind them?'}" id="grind" open="{open_grind}" disabled="{plan.coffee === 'Capsules' ? true : false}">
					<input type="radio" name="grind" id="wholebean" on:change="{() => setQuestion('Wholebean', 'grind')}" checked="{plan.grind === 'wholebean' ? true : false}" />
					<input type="radio" name="grind" id="grind-filter" on:change="{() => setQuestion('Filter', 'grind')}" checked="{plan.grind === 'filter' ? true : false}" />
					<input type="radio" name="grind" id="cafetiere" on:change="{() => setQuestion('Cafetiére', 'grind')}" checked="{plan.grind === 'cafetiere' ? true : false}" />
					<label for="wholebean"
						><h4>Wholebean</h4>
						<p>Best choice if you cherish the full sensory experience</p>
					</label>
					<label for="grind-filter"
						><h4>Filter</h4>
						<p>For drip or pour-over coffee methods such as V60 or Aeropress</p></label
					>
					<label for="cafetiere"
						><h4>Cafetiére</h4>
						<p>Course ground beans specially suited for french press coffee</p></label
					>
				</Question>
				<Question h2="{'How often should we deliver?'}" id="frequency" open="{open_frequency}">
					<input type="radio" name="frequency" id="week" on:change="{() => setQuestion('Every week', 'frequency')}" checked="{plan.frequency === 'week' ? true : false}" />
					<input type="radio" name="frequency" id="two-weeks" on:change="{() => setQuestion('Every 2 weeks', 'frequency')}" checked="{plan.frequency === 'two weeks' ? true : false}" />
					<input type="radio" name="frequency" id="month" on:change="{() => setQuestion('Every month', 'frequency')}" checked="{plan.frequency === 'month' ? true : false}" />
					<label for="week"
						><h4>Every week</h4>
						<p>$7.20 per shipment. Includes free first-class shipping.</p>
					</label>
					<label for="two-weeks"
						><h4>Every 2 weeks</h4>
						<p>$9.60 per shipment. Includes free priority shipping.</p>
					</label>
					<label for="month"
						><h4>Every month</h4>
						<p>$12.00 per shipment. Includes free priority shipping.</p>
					</label>
				</Question>
			</div>

			<div class="summary">
				<p>order summary</p>
				<p class="summary-text">
					“I drink my coffee {plan.coffee === "Capsules" ? "using" : "as"} <span>{plan.coffee}</span>, with a <span>{plan.beans}</span> type of bean.
					{#if plan.coffee === "Capsules"}
						Sent
					{:else}
						<span>{plan.quantity}</span> ground ala <span>{plan.grind}</span>, sent
					{/if}
					to me <span>{plan.frequency}</span>.”
				</p>
			</div>

			<button type="submit">Create my plan!</button>
		</div>
	</form>
</main>

<style lang="scss">
	@import "$lib/styles/variables.scss";

	main {
		@include size(100%, fit-content);
		@include flex(center, center, column, 168px);
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
			background-image: url("$lib/assets/plan/desktop/image-hero-blackcup.jpg");
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
			background-image: url("$lib/assets/plan/tablet/image-hero-blackcup.jpg");
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
			background-image: url("$lib/assets/plan/mobile/image-hero-blackcup.jpg");
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

	form {
		padding-inline: 80px;

		.legend {
			@include flex(start, start, column, 24px);
			@include size(255px, fit-content);
			div:not(.line) {
				@include h4();
				@include transition(all);
				color: $darkGreyBlue;
				cursor: pointer;

				span {
					padding-right: 4px;
					color: $darkCyan;
				}

				&.undecided {
					opacity: 0.5;
				}
				&.disabled {
					cursor: not-allowed;
					opacity: 0.25;
				}
			}

			.line {
				@include size(100%, 1px);
				background-color: rgba($grey, 0.25);
			}
		}

		.content {
			@include size(100%, fit-content);
			@include flex(center, end, column, 80px);

			.questions {
				@include size(100%, fit-content);
				@include flex(center, end, column, 36px);
				max-width: 1280px;
				input {
					display: none;
				}

				label {
					@include flex(start, start, column, 24px);
					@include size(auto, 100%);
					@include transition(all);
					padding: 28px;
					border-radius: 8px;
					background-color: #f4f1eb;
					color: $darkGreyBlue;
					cursor: pointer;

					h4 {
						@include h4();
					}

					p {
						@include p();
					}
				}

				#capsule:checked ~ label[for="capsule"],
				#filter:checked ~ label[for="filter"],
				#espresso:checked ~ label[for="espresso"],
				#single-origin:checked ~ label[for="single-origin"],
				#decaf:checked ~ label[for="decaf"],
				#blended:checked ~ label[for="blended"],
				#quarter:checked ~ label[for="quarter"],
				#half:checked ~ label[for="half"],
				#one:checked ~ label[for="one"],
				#wholebean:checked ~ label[for="wholebean"],
				#grind-filter:checked ~ label[for="grind-filter"],
				#cafetiere:checked ~ label[for="cafetiere"],
				#week:checked ~ label[for="week"],
				#two-weeks:checked ~ label[for="two-weeks"],
				#month:checked ~ label[for="month"] {
					background: $darkCyan;
					color: #ffffff;
				}
			}

			.summary {
				border-radius: 8px;
				background-size: cover;
				p {
					@include p();
					text-transform: uppercase;
					opacity: 0.5;
				}

				.summary-text {
					@include h4();
					opacity: 1;

					span {
						color: $darkCyan;
					}
				}

				@media (width >= $tablet) {
					@include size(100%, auto);
					@include flex(start, start, column, 12px);
					max-width: 725px;
					background-image: url("$lib/assets/plan/desktop/bg-order-summary.png");
					padding: 47px 64px;
				}

				@media (width < $tablet) {
					@include size(100%, auto);
					@include flex(start, start, column, 12px);
					background-image: url("$lib/assets/plan/mobile/bg-order-summary.png");

					padding: 32px 25px;
				}
			}

			button {
				@include button();
			}
		}

		@media (width >= $desktop) {
			@include flex(start, start);
			@include size(100%, auto);
		}

		@media (width < $desktop) {
			overflow-x: hidden;
			padding-inline: 0px;
			.legend {
				display: none;
			}
		}
	}

	dialog {
		@include flex(center, center);
		min-width: 100vw;
		min-height: 100vh;
		background-color: rgba(black, 0.5);
		z-index: 1000;
		position: fixed;
		top: 0;
		border: none;

		@media (width >= $desktop) {
			.popup {
				@include size(fit-content, fit-content);
				@include flex(start, start, column);
				background-color: $bg;
				border-radius: 10px 10px 8px 8px;
				max-width: 540px;

				.popup-header {
					@include size(100%, 136px);
					@include flex(start, center);
					padding-inline: 56px;

					background-image: url("$lib/assets/plan/desktop/bg-modal-top.png");
					border-radius: 8px 8px 0 0;
					color: $bg;
					@include h2();
				}

				.popup-content {
					color: $grey;
					padding: 56px;

					.plan {
						@include h4();

						span {
							color: $darkCyan;
						}
					}

					.confirmation {
						@include p();
						margin-top: 46px;
					}
				}

				.popup-footer {
					@include size(100%, auto);
					@include flex(space-between, center);
					padding: 56px;

					.price {
						@include h3();
						color: $darkGreyBlue;
					}

					button {
						@include button();
					}
				}
			}
		}

		@media ($tablet < width < $desktop) {
			.popup {
				@include size(fit-content, fit-content);
				@include flex(start, start, column);
				background-color: $bg;
				border-radius: 10px 10px 8px 8px;
				max-width: 540px;

				.popup-header {
					@include size(100%, 136px);
					@include flex(start, center);
					padding-inline: 56px;

					background-image: url("$lib/assets/plan/desktop/bg-modal-top.png");
					border-radius: 8px 8px 0 0;
					color: $bg;
					@include h2();
				}

				.popup-content {
					color: $grey;
					padding: 56px;

					.plan {
						@include h4();

						span {
							color: $darkCyan;
						}
					}

					.confirmation {
						@include p();
						margin-top: 46px;
					}
				}

				.popup-footer {
					@include size(100%, auto);
					@include flex(space-between, center);
					padding: 56px;

					.price {
						@include h3();
						color: $darkGreyBlue;
					}

					button {
						@include button();
					}
				}
			}
		}

		@media (width < $tablet) {
			.popup {
				@include size(fit-content, fit-content);
				@include flex(start, start, column);
				background-color: $bg;
				border-radius: 10px 10px 8px 8px;
				max-width: 90vw;

				.popup-header {
					@include size(100%, 136px);
					@include flex(start, center);
					padding-inline: 32px;

					background-image: url("$lib/assets/plan/desktop/bg-modal-top.png");
					border-radius: 8px 8px 0 0;
					color: $bg;
					@include h2(28px);
				}

				.popup-content {
					color: $grey;
					padding: 32px 32px 0 32px;

					.plan {
						@include h4(18px);

						span {
							color: $darkCyan;
						}
					}

					.confirmation {
						@include p(15px);
						margin-top: 12px;
					}
				}

				.popup-footer {
					@include size(100%, auto);
					@include flex(space-between, center);
					padding: 32px;

					.price {
						@include h3(24px);
						color: $darkGreyBlue;
					}

					button {
						@include button("small");
					}
				}
			}
		}
	}
</style>
