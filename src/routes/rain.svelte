<script>
	const day = new Date().getDay();
	const dayArr = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
	import { onMount } from 'svelte';

	let characters = ['💧'];

	let confetti = new Array(50)
		.fill()
		.map((_, i) => {
			return {
				character: characters[i % characters.length],
				x: Math.random() * 100,
				y: -20 - Math.random() * 100,
				r: 1,
				rotation: 0
			};
		})
		.sort((a, b) => a.r - b.r);

	onMount(() => {
		let frame;

		function loop() {
			frame = requestAnimationFrame(loop);

			confetti = confetti.map((emoji) => {
				emoji.y += 0.3 * emoji.r;
				if (emoji.y > 120) emoji.y = -20;
				return emoji;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

<div class="absolute w-screen h-screen">
	<div class="relative w-full h-full overflow-hidden">
		{#each confetti as c}
			<span
				class="absolute select-none text-base"
				style="left: {c.x}%; top: {c.y}%; transform: scale({c.r}) rotate({c.rotation}deg)"
			>
				{c.character}
			</span>
		{/each}
	</div>
</div>
