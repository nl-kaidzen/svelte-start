<script>

	let monthArray = ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", '11', "12"];
	let yearsArray = [2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2025, 2026];

	let cardNum = '';
	let currentMask = ["****", "****", "****", "****"];
	let currentNumber = "";

	let cardHolderName = "";
	let expiresMonth = "";
	let expiresYear = "";

	function cardNumberHandler(event) {
		cardNum = event.target.value;
		console.log(cardNum);
	}

	function renderNumInCardNumber () {

	}

	function splitNumberGroup(group) {
		let numbersInGroup = group.split();
		console.log(numbersInGroup);
		return numbersInGroup;
	}
</script>

<main>
	<section class="pay-form">
		<div class="pay-form__card  card">
			<div class="card-number__wrapper">
				<span class="card__num-label">Card number</span>
				<span class="card-number__el">{cardNum}</span>
			</div>
			<div class="card__info">
				<div class="card__holder">
					<span class="card__holder-label">Card holder</span>
					<span class="card__holder-name">{cardHolderName.toUpperCase()}</span>
				</div>
				<div class="card__expires">
					<span class="card__expires-label">Expires</span>
					<span class="card__expires-date">{expiresMonth}/{expiresYear}</span>
				</div>

			</div>
		</div>
		<form action="" class="pay-form__form  form">
			<label>
				<span class="input-title  form__card-number">Card number</span>
				<input 
					type="text" 
					class="input" 
					on:input={cardNumberHandler}
					maxlength="16">
			</label>

			<label>
				<span class="input-title  form__card-name">Card name</span>
				<input type="text" class="input" bind:value={cardHolderName}>
			</label>

			<div class="wrapper">
				<label>
					<span class="input-title  form__card-month">Month</span>
					<select name="" id="" class="select" bind:value={expiresMonth}>
						{#each monthArray as monthNumber}
							<option value="{monthNumber}">{monthNumber}</option>
						{/each}
					</select>
				</label>

				<label>
					<span class="input-title  form__card-year">Year</span>
					<select name="" id="" class="select" bind:value={expiresYear}>
						{#each yearsArray as yearNumber}
							<option value="{yearNumber}">{yearNumber}</option>
						{/each}
					</select>
				</label>

				<label>
					<span class="input-title  form__card-cvv">CVV</span>
					<input type="text" class="input">
				</label>
			</div>
			<button class="form__submit">SUBMIT</button>
		</form>
	</section>
</main>

<style>
	* {
		box-sizing: border-box;
	}
	main {
		width: 100%;
		height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.pay-form {
		display: flex;
		flex-direction: column;
		width: 400px;
		height: 500px;
		padding: 20px;
		border: 1px solid #444444;
		border-radius: 10px;
		position: relative;
	}

	.pay-form__card {
		width: 300px;
		height: 175px;
		border-radius: 10px;
		background-color: rgb(11, 25, 71);
		position: absolute;
		top: 0;
		left: 50%;
		transform: translate(-50%, -50%);
	}

	.pay-form__form {
		display: flex;
		flex-direction: column;
		margin-top: 100px;
	}

	.wrapper {
		display: flex;
		justify-content: space-between;
	}

	label {
		display: flex;
		flex-direction: column;
		margin-bottom: 15px;
	}
	
	.input-title {
		font-size: 12px;
		margin-bottom: 5px;
	}

	.input,
	.select {
		border: 1px solid lightgray;
		background-color: white;
		font-size: 15px;
		line-height: 1;
		color: #444444;
		padding: 8px 10px;
		border-radius: 5px;
	}

	.input:focus,
	.select:focus {
		outline: none;
		border-color: #4da6ff;
	}

	.wrapper label {
		width: 25%;
	}

	.form__submit {
		color: white;
		background-color: #1a1aff;
		width: 100;
		text-transform: uppercase;
		display: flex;
		justify-content: center;
		align-items: center;
		cursor: pointer;
		border-radius: 5px;
		user-select: none;
		transition: all 0.5s ease;
	}

	.form__submit:hover,
	.form__submit:focus {
		background-color: rgb(11, 25, 71);
	}

	.form__submit:active {
		background-color: #1a1aff;
	}

	/* Here starts CSS for Card */

	.card-number__wrapper {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: flex-start;

		margin: 65px 20px 0 20px;
		height: 50px;
	}

	.card-number__el {
		color: white;
		font-size: 16px;
		line-height: 1;
		transition: all 0.7s ease-in;
	}

	.card__info {
		display: flex;
		margin-top: 10px;
		padding: 0 20px;
		justify-content: space-between;
	}

	.card__holder {
		width: 70%;
	}

	.card__expires {
		width: 20%;
	}

	.card__num-label,
	.card__holder-label,
	.card__expires-label {
		font-size: 12px;
		color: grey;
		display: block;
	}

	.card__holder-name,
	.card__expires-date {
		color: white;
	}
</style>