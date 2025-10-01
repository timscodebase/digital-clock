<script lang="ts">
	import DigitalClock from './digital-clock.svelte';

	const countdownTarget = new Date(Date.now() + 48 * 60 * 60 * 1000);
</script>

<svelte:head>
	<title>Digital Clock</title>
	<meta name="description" content="A digital clock and countdown built with Svelte 5" />
</svelte:head>

<div class="container">
	<div>
		<h2>Current Time (Custom Style)</h2>
		<DigitalClock
			litColor="#00ffff"
			offColor="#1a202c"
			backgroundColor="#001f3f"
			colonBlink={true}
		/>
	</div>
	<div>
		<h2>48 Hour Countdown (Default Style)</h2>
		<DigitalClock targetDate={countdownTarget} skew={-5} />
	</div>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 100%;
		flex: 1;
		gap: 3rem;
	}
	h2 {
		text-align: center;
		font-family: Arial, sans-serif;
		margin-bottom: 1rem;
	}
</style>