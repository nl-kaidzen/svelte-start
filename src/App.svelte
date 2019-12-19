<script>

	let monthArray = ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", '11', "12"];
	let yearsArray = [2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2025, 2026];

	let cardNum = '#### #### #### ####';
	let currentMask = ["#", "#", "#", "#", " ", "#", "#", "#", "#", " ", "#", "#", "#", "#", " ", "#", "#", "#", "#"];
	let currentNumber = [];
	let numbersArray = []

	let cardHolderName = "Firstname lastname";
	let expiresMonth = "MM";
	let expiresYear = "YYYY";

	let re = /[0-9]/;

	function splitCardNumberToArray(number) {
		currentMask.forEach((it, index) => currentNumber[index] = it);
		numbersArray = number.split("");
		numbersArray.forEach((it, index) => currentNumber[index] = it);
	};

	function keyPressHendler(e) {
		let keyValue = e.data;
		let keyFunction = e.inputType;
		let spaceNumber = 0;

		if (keyFunction === "deleteContentBackward") {
			cardNum = e.target.value;
			let l = e.target.value.length;

			if ((l == 5) || (l == 10) || (l == 15)) {
					e.target.value = e.target.value.slice(0, -1);
					cardNum = e.target.value;
				};
		} else {
			if ((keyValue.search(re) != -1) === true) { 
				cardNum = e.target.value;
				let l = e.target.value.length;

				if ((l == 4) || (l == 9) || (l == 14)) {
					e.target.value = e.target.value + ' ';
					cardNum = e.target.value;
				};
			} else {
				e.target.value = e.target.value.slice(0, -1);
				cardNum = e.target.value;
			}
		}
	};

	$: {
		splitCardNumberToArray(cardNum);
	}
</script>

<main>
	<section class="pay-form">
		<div class="pay-form__card  card">
			<div class="card-number__wrapper">
				{#each currentNumber as item, i}
					{#if (item !== '')}
						<span class="card-number__el">{item}</span>
					{:else}
						<div class="card-number__spacer"></div>
					{/if}
				{/each}
			</div>
			<div class="card__info">
				<div class="card__holder">
					<span class="card__holder-label">Card holder</span>
					<span class="card__holder-name">{cardHolderName.toUpperCase()}</span>
				</div>
				<div class="card__expires">
					<span class="card__expires-label">Expires</span>
					<span class="card__expires-date">{expiresMonth}/{expiresYear.toString().slice(2, 4)}</span>
				</div>

			</div>
		</div>
		<form action="" class="pay-form__form  form">
			<label>
				<span class="input-title  form__card-number">Card number</span>
				<input 
					type="text" 
					class="input"
					on:input={keyPressHendler}
					maxlength="19"
					pattern="[1-9]{1}[0-9]{3}\s[1-9]{1}[0-9]{3}\s[1-9]{1}[0-9]{3}\s[1-9]{1}[0-9]{3}">
			</label>

			<label>
				<span class="input-title  form__card-name">Card name</span>
				<input type="text" class="input" 
					   on:input= {(e) => cardHolderName = e.target.value }>
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
	@import url("https://fonts.googleapis.com/css?family=Source+Code+Pro:400,500,600,700|Source+Sans+Pro:400,600,700&display=swap");

	* {
		box-sizing: border-box;
	}
	main {
		width: 100%;
		height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
		font-family: "Source Sans Pro", monospace;
  		font-size: 16px;
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
		width: 330px;
		height: 210px;
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
		transition: all 0.3s ease-in-out;
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
		flex-direction: row;
		justify-content: space-between;
		align-items: center;

		margin: 80px 20px 0 20px;
		height: 50px;
	}

	.card-number__el {
		display: block;
		width: 5%;
		flex-shrink: 0;
		color: white;
		font-size: 20px;
		line-height: 1;
		transition: all 0.7s ease-in-out;
	}

	.card-number__spacer {
		display: flex;
		flex-grow: 1;
	}

	.card__info {
		display: flex;
		margin-top: 15px;
		padding: 0 20px;
		justify-content: space-between;
	}

	.card__holder {
		width: 70%;
	}

	.card__expires {
		width: 25%;
	}

	.card__holder-label,
	.card__expires-label {
		font-size: 13px;
		color: white;
		display: block;
		opacity: 0.7;
		margin-bottom: 6px;
	}

	.card__holder-name,
	.card__expires-date {
		color: white;
	}
</style>