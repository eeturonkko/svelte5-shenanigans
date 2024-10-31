<script lang="ts">
	let weight = $state<number>();
	let height = $state<number>();
	let bmi = $state<number>(0);

	function calculateBMI() {
		if (!weight || !height) {
			return;
		}
		return (bmi = weight / ((height / 100) * (height / 100)));
	}
</script>

<main class="h-screen">
	<section
		class="container mx-auto mt-24 max-w-xl rounded-md border border-black bg-gray-200 p-4 drop-shadow-md"
	>
		<div class="max-w- flex flex-col border">
			<h2 class="mb-2 font-semibold">BMI Calculator</h2>
			<div class="mb-4 flex flex-col gap-1">
				<label class="font-semibold" for="">Weight (kg)</label>
				<input bind:value={weight} type="text" class="max-w-xs" />
				<label class="font-semibold" for="">Height (cm)</label>
				<input bind:value={height} type="text" class="max-w-xs" />
				<button
					class="px-58 mt-4 max-w-32 text-nowrap rounded bg-white font-semibold"
					onclick={calculateBMI}>Calculate BMI</button
				>
			</div>
			<div class="mb-2">
				{#if bmi > 0}
					<p class="font-semibold">Your BMI is: {bmi.toFixed(1)}</p>
				{/if}
			</div>
			<a class="max-w-16 rounded bg-white p-2 font-semibold text-black" href="/">Home</a>
		</div>
	</section>
</main>
