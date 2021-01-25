<script>
	const pricePerDay = 11;

	let selectedMonth = 'custom';
	let customWorkDays = 20;
	let vacationDays = 0;
	let sickDays = 0;

	const months = [
		{ key: 'custom', label: 'Custom' },
		{ key: '2021/01', label: 'Enero 2021', workDays: 19 },
		{ key: '2021/02', label: 'Febrero 2021', workDays: 20 },
		{ key: '2021/03', label: 'Marzo 2021', workDays: 22 },
		{ key: '2021/04', label: 'Abril 2021', workDays: 20 },
		{ key: '2021/05', label: 'Mayo 2021', workDays: 21 },
	];

	$: workDays = months.find(m => m.key === selectedMonth)?.workDays ?? customWorkDays;
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
		{#each months as month (month.key)}
		<option value={month.key}>{month.label}</option>
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
