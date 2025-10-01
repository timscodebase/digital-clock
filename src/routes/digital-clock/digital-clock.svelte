<script lang="ts">
	import Digit from './digit.svelte';
	import Colon from './colon.svelte';

	type Props = {
		targetDate?: Date;
		litColor?: string;
		offColor?: string;
		backgroundColor?: string;
		colonBlink?: boolean;
		skew?: 0 | -1 | -2 | -3 | -4 | -5 | -6;
	};

	// Set default values for the new props
	let {
		targetDate,
		litColor = '#ff8c00', // Default lit color (orange)
		offColor = '#282828', // Default off color (dark gray)
		backgroundColor = '#000', // Default background (black)
		colonBlink = false, // Default to not blinking
		skew = -6 // Default skew
	}: Props = $props();

	let time = $state({ h: 0, m: 0, s: 0 });

	$effect(() => {
		const update = () => {
			const now = new Date();
			if (targetDate) {
				const remaining = Math.max(0, targetDate.getTime() - now.getTime());
				time.h = Math.floor((remaining / (1000 * 60 * 60)) % 24);
				time.m = Math.floor((remaining / (1000 * 60)) % 60);
				time.s = Math.floor((remaining / 1000) % 60);
			} else {
				time.h = now.getHours();
				time.m = now.getMinutes();
				time.s = now.getSeconds();
			}
		};
		update();
		const interval = setInterval(update, 1000);
		return () => clearInterval(interval);
	});

	const d1 = $derived(Math.floor(time.h / 10));
	const d2 = $derived(time.h % 10);
	const d3 = $derived(Math.floor(time.m / 10));
	const d4 = $derived(time.m % 10);
	const d5 = $derived(Math.floor(time.s / 10));
	const d6 = $derived(time.s % 10);
</script>

<div class="clock" style="--background-color: {backgroundColor}; --skew: {skew}deg;">
	<Digit number={d1} {litColor} {offColor} />
	<Digit number={d2} {litColor} {offColor} />
	<Colon {litColor} {offColor} blink={colonBlink} />
	<Digit number={d3} {litColor} {offColor} />
	<Digit number={d4} {litColor} {offColor} />
	<Colon {litColor} {offColor} blink={colonBlink} />
	<Digit number={d5} {litColor} {offColor} />
	<Digit number={d6} {litColor} {offColor} />
</div>

<style>
	.clock {
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 20px;
		border-radius: 10px;
		gap: 5px;
		background: var(--background-color); /* Use the CSS variable */
		filter: blur(1px);
		opacity: 0.8;
		transform: skewX(var(--skew));
	}
</style>