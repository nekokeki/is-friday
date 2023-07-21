<script>
	import { onMount } from 'svelte';

	let day;
	const dayArr = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
	const wait = () => new Promise((res) => setTimeout(res, 1000));

	onMount(() => {
		day = new Date().getDay();
	});

	function typewriter(node, { speed = 1 }) {
		const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

		if (!valid) {
			throw new Error(`This transition only works on elements with a single text node child`);
		}

		const text = node.textContent;
		const duration = text.length / (speed * 0.01);

		return {
			duration,
			tick: (t) => {
				const i = Math.trunc(text.length * t);
				node.textContent = text.slice(0, i);
			}
		};
	}
</script>

<div class="flex-grow flex flex-col items-center justify-center">
	<div class="container mx-auto text-center h-full">
		<h1 class="text-7xl">
			Today
			{#await wait()}
				<span transition:typewriter>__</span>
			{:then}
				<span transition:typewriter>{day === 5 ? 'is' : 'is not'}</span>
			{/await}
			Friday
		</h1>
		{#if day !== 5}
			<h2>Today is {dayArr[day]}</h2>
		{/if}
	</div>
</div>
