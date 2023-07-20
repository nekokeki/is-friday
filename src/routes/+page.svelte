<script>
	const day = new Date().getDay();
	const dayArr = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
</script>

<div class="flex-grow flex flex-col items-center justify-center">
	<div class="container mx-auto text-center h-full">
		<h1 class="text-7xl">Today {day === 5 ? 'is' : 'is not'} Friday</h1>
		{#if day !== 5}
			<h2>Today is {dayArr[day]}</h2>
		{/if}
	</div>
</div>
