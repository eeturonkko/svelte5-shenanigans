<script lang="ts">
	let count = $state(0);
	let doubled = $derived(count * 2);

	function increment() {
		count += 1;
	}

	function reset() {
		count = 0;
	}
</script>

<main class="h-screen">
	<section
		class="container mx-auto mt-24 max-w-xl rounded-md border border-black bg-gray-200 p-4 drop-shadow-md"
	>
		<div class="max-w- flex flex-col border">
			<h2 class="font-semibold">Counter</h2>
			<div class="mt-2 flex gap-6 drop-shadow-lg">
				<input class="rounded bg-white p-1" type="text" bind:value={count} disabled />
				<button onclick={increment} class="rounded bg-white p-1 font-semibold">Count</button>
			</div>
			<div class="mb-8 mt-2 flex gap-6 drop-shadow-lg">
				<input class="rounded bg-white p-1" type="text" value={doubled} disabled />
				<button onclick={reset} class="rounded bg-white p-1 font-semibold">Reset</button>
			</div>
		</div>
		<a class="rounded bg-white p-2 font-semibold text-black" href="/">Home</a>
	</section>
</main>
