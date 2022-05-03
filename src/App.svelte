<script>
	let years = 15;
	let loanAmount = 200000;
	let interestRateIn = 200;

	var formatter = new Intl.NumberFormat("en-US", {
		style: "currency",
		currency: "USD"
	});

	$: interestRate = interestRateIn / 100;
	$: totalPayments = years * 12;
	$: monthlyInterestRate = interestRate / 100 / 12;
	$: monthlyPayments = 
		(loanAmount * 
		 Math.pow(1 + monthlyInterestRate,
		 totalPayments) *
		 monthlyInterestRate) / 
		(Math.pow(1 + monthlyInterestRate,
		 totalPayments) - 1);
	$: totalPay = monthlyPayments * totalPayments;
	$: interestPaid = totalPaid - loanAmount;
</script>

<main class='container'>
	<div class="row">
		<h1>Mortgage Calculator</h1>
	</div>
	<div class="row">
		<label for="">Loan Amount</label>
		<input type="number" name="" 
		placeholder="Enter loan amount" 
		bind:value={loanAmount}
		min="1" class="u-full-width">
	</div>
	<div class="row">
		<div class="columns six">
			<label for="">Years</label>
			<input type="range" min="1" max="50" 
			name="" id="" class="u-full-width" bind:value={years}>
		</div>
		<div class="columns six outputs">
			{years} Years
		</div>
	</div>
	<div class="row">
		<div class="columns six">
			<label for="">Interest Rate</label>
			<input type="range" min="1" max="2000" 
			name="" id="" class="u-full-width" bind:value={interestRateIn}>
		</div>
		<div class="columns six outputs">
			{interestRate.toFixed(2)}%
		</div>
	</div>

	<div class="row outputs">Monthly Payments: {formatter.format(monthlyPayments)}</div>
	<div class="row outputs">Total Payment: {formatter.format(totalPay)}</div>
	<div class="row outputs">Interest Paid: {formatter.format(interestPaid)}</div>

</main>

<style>
	.outputs{
		font-size: 20px;
		border: solid black 2px;
		margin-top: 15px;
		text-align: center
	}
</style>
