<script lang="ts">
	const segmentMap = new Map([
		[0, ['A', 'B', 'C', 'D', 'E', 'F']],
		[1, ['B', 'C']],
		[2, ['A', 'B', 'D', 'E', 'G']],
		[3, ['A', 'B', 'C', 'D', 'G']],
		[4, ['B', 'C', 'F', 'G']],
		[5, ['A', 'C', 'D', 'F', 'G']],
		[6, ['A', 'C', 'D', 'E', 'F', 'G']],
		[7, ['A', 'B', 'C']],
		[8, ['A', 'B', 'C', 'D', 'E', 'F', 'G']],
		[9, ['A', 'B', 'C', 'D', 'F', 'G']]
	]);

	type Props = {
		number: number;
		litColor: string;
		offColor: string;
	};
	let { number, litColor, offColor }: Props = $props();

	const litSegments = $derived(segmentMap.get(number) || []);
	const allSegments = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
</script>

<div class="digit" style="--lit-color: {litColor}; --off-color: {offColor};">
	{#each allSegments as segment}
		<div class="segment {segment.toLowerCase()}" class:lit={litSegments.includes(segment)}></div>
	{/each}
</div>

<style>
	.digit {
		position: relative;
		width: 60px;
		height: 100px;
	}
	.segment {
		position: absolute;
		background: var(--off-color);
		border-radius: 3px;
		transition: background-color 0.1s;
	}
	.segment.lit {
		background: var(--lit-color);
		box-shadow: 0 0 8px var(--lit-color);
	}
	/* Segment positioning */
	.a { top: 0; left: 10px; width: 40px; height: 10px; }
	.b { top: 10px; left: 50px; width: 10px; height: 40px; }
	.c { top: 50px; left: 50px; width: 10px; height: 40px; }
	.d { top: 90px; left: 10px; width: 40px; height: 10px; }
	.e { top: 50px; left: 0; width: 10px; height: 40px; }
	.f { top: 10px; left: 0; width: 10px; height: 40px; }
	.g { top: 45px; left: 10px; width: 40px; height: 10px; }
</style>