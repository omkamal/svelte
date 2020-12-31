<script>
	export let name;
	let interestRate = 3;
	let loanAmount = 200000;
	let years = 30;
	const MONTHS_PER_YEAR = 12;

	$: months = years * MONTHS_PER_YEAR;
	$: monthlyInterestRate = interestRate / 100 / MONTHS_PER_YEAR;
	$: numerator = loanAmount * monthlyInterestRate;
	$: denominator = 1 - (1 + monthlyInterestRate) ** -months;
	$: payment = !loanAmount || !years ? 0: 
	interestRate ? numerator / denominator :
	loanAmount / months;

</script>

<main>
	<label for="loan">Loan Amount</label>
	<input id="loan" type="number" bind:value={loanAmount}>

	<label for="interest">Interest Rate</label>
	<input id="interest" type="number" bind:value={interestRate}>

	<label for="years">Years</label>
	<input id="years" type="number" bind:value={years}>

	<div>
		monthlyInterestRate: {monthlyInterestRate} 
		<br>
		numerator: {numerator}

		<p>
			Montly Payment: ${payment.toFixed(2)}
		</p>
		
	</div>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>