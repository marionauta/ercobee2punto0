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

<div>
	Mes:
	<select bind:value={selectedMonth}>
		{#each months as month}
		<option value={month.label}>{month.label}</option>
		{/each}
	</select>
</div>

<div>
	Días laborables:
	{#if selectedMonth === 'custom'}
	<input bind:value={customWorkDays}>
	{:else}
	<input bind:value={workDays} disabled>
	{/if}
</div>

<div>
	Días de vacaciones:
	<input bind:value={vacationDays}>
</div>

<div>
	Días de baja:
	<input bind:value={sickDays}>
</div>

<div>
	<b>Total: {total}</b>
</div>
