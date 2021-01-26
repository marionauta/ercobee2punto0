<script>
	const pricePerDay = 11;

	let selectedMonth = 'custom';
	let customWorkDays = 20;
	let vacationDays = 0;
	let sickDays = 0;

	const months = [
		{ key: 'custom', label: 'Custom' },
		{ key: '2021', label: '2021', separator: true },
		{ key: '2021/01', label: 'Enero', workDays: 19 },
		{ key: '2021/02', label: 'Febrero', workDays: 20 },
		{ key: '2021/03', label: 'Marzo', workDays: 22 },
		{ key: '2021/04', label: 'Abril', workDays: 19 },
		{ key: '2021/05', label: 'Mayo', workDays: 21 },
		{ key: '2021/06', label: 'Junio', workDays: 21 },
		{ key: '2021/07', label: 'Julio', workDays: 22 },
		{ key: '2021/08', label: 'Agosto', workDays: 21 },
		{ key: '2021/09', label: 'Septiembre', workDays: 22 },
		{ key: '2021/10', label: 'Octubre', workDays: 20 },
		{ key: '2021/11', label: 'Noviembre', workDays: 21 },
		{ key: '2021/12', label: 'Diciembre', workDays: 21 },
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
	.center {
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
		<option value={month.key} disabled={month.separator}>{month.label}</option>
		{/each}
	</select>

	<span>Días laborables:</span>
	{#if selectedMonth === 'custom'}
	<input type=number bind:value={customWorkDays}>
	{:else}
	<input type=number value={workDays} disabled>
	{/if}

	<span>Días de vacaciones:</span>
	<input type=number bind:value={vacationDays}>

	<span>Días de baja:</span>
	<input type=number bind:value={sickDays}>

	<b class=center>Total: {total}€</b>
	<a class=center href=https://www.calendarioslaborales.com/calendario-laboral-sevilla-2021.htm target=_blank>
		Calendario laboral
	</a>
	<a class=center href=https://github.com/marionauta/ercobee2punto0 target=_blank>
		github repo
	</a>
</div>
