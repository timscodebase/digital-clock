<script lang="ts">
	type Props = {
		litColor: string;
		offColor: string;
		blink: boolean;
	};
	let { litColor, offColor, blink }: Props = $props();
</script>

<div class="colon-container">
	<div class="dot" style="--lit-color: {litColor}; --off-color: {offColor};" class:blinking={blink}></div>
	<div class="dot" style="--lit-color: {litColor}; --off-color: {offColor};" class:blinking={blink}></div>
</div>

<style>
	.colon-container {
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		height: 100px;
		width: 20px;
		align-items: center;
	}
	.dot {
		width: 10px;
		height: 10px;
		border-radius: 50%;
		background-color: var(--lit-color);
		box-shadow: 0 0 8px var(--lit-color);
	}
	/* Add the blinking animation */
	.dot.blinking {
		animation: blink-animation 1s step-end infinite;
	}
	@keyframes blink-animation {
		50% {
			background-color: var(--off-color);
			box-shadow: none;
		}
	}
</style>