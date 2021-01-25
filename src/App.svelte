<script>
	const pricePerDay = 11;

	let selectedMonth = 'custom';
	let customWorkDays = 20;
	let vacationDays = 0;
	let sickDays = 0;

	const months = [
		{ label: 'custom', workDays: undefined },
		{ label: 'enero', workDays: 19 },
		{ label: 'febrero', workDays: 20 },
		{ label: 'marzo', workDays: 22 },
		{ label: 'abril', workDays: 20 },
		{ label: 'mayo', workDays: 21 },
	];

	$: workDays = months.find(m => m.label === selectedMonth)?.workDays ?? customWorkDays;
	$: daysWithBenefits = workDays - vacationDays - sickDays;
	$: total = Math.min(220, pricePerDay * daysWithBenefits);
</script>

<style>
	.container {
		display: grid;
		grid-template-columns: 1fr 1fr;
		row-gap: .75rem;
		max-width: 35rem;
		margin: 0 auto;
	}
	.container * {
		align-self: center;
		margin: 0;
	}
	.total {
		font-weight: bold;
		text-align: center;
		line-height: 2rem;
		grid-column-start: 1;
		grid-column-end: 3;
	}
</style>

<div class=container>
	<span>Mes:</span>
	<select bind:value={selectedMonth}>
		{#each months as month}
		<option value={month.label}>{month.label}</option>
		{/each}
	</select>

	<span>Días laborables:</span>
	{#if selectedMonth === 'custom'}
	<input type=number bind:value={customWorkDays}>
	{:else}
	<input type=number bind:value={workDays} disabled>
	{/if}

	<span>Días de vacaciones:</span>
	<input type=number bind:value={vacationDays}>

	<span>Días de baja:</span>
	<input type=number bind:value={sickDays}>

	<span class=total>Total: {total}€</span>
</div>
