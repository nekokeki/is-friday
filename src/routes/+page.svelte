<script>
	import { typewriter } from '$lib/typewriter';
	import { onMount } from 'svelte';

	let day;
	let today;

	const dayArr = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
	const wait = () => new Promise((res) => setTimeout(res, 1000));

	onMount(() => {
		day = new Date().getDay();
	});
</script>

<div class="flex-grow flex flex-col items-center justify-center">
	<div class="container mx-auto text-center h-full">
		<h1 class="text-7xl">
			Today
			{#await wait()}
				<span transition:typewriter>__</span>
			{:then}
				<span transition:typewriter on:introend={() => wait().then(() => (today = dayArr[day]))}>
					{day === 5 ? 'is' : 'is not'}
				</span>
			{/await}
			Friday
		</h1>
		{#if today && day !== 5}
			<h2 transition:typewriter>{'Today is ' + today}</h2>
		{/if}
	</div>
</div>
