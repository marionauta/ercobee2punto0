<script>
	let workDays = undefined;
	let customWorkDays = 20;
	let vacationDays = 0;
	let sickDays = 0;

	const pricePerDay = 11;

	const months = [
		{ label: 'custom', workDays: undefined },
		{ label: 'enero', workDays: 19 },
		{ label: 'febrero', workDays: 20 },
		{ label: 'marzo', workDays: 22 },
		{ label: 'abril', workDays: 20 },
		{ label: 'mayo', workDays: 21 },
	];

	$: daysWithBenefits = (workDays ?? customWorkDays) - vacationDays - sickDays;
	$: total = Math.min(220, pricePerDay * daysWithBenefits);
</script>

<div>
	Mes:
	<select bind:value={workDays}>
		{#each months as month}
		<option value={month.workDays}>{month.label}</option>
		{/each}
	</select>
</div>

<div>
	Días laborables:
	{#if !workDays}
	<input value={customWorkDays}>
	{:else}
	<input value={workDays} disabled>
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
