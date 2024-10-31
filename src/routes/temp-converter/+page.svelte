<script lang="ts">
	class Temperature {
		#c = $state<number>();
		#f = $state<number>();

		get c() {
			return this.#c;
		}

		set c(c) {
			this.#c = Math.ceil(c!!);
			this.#f = Math.ceil(c!! * (9 / 5) + 32);
		}

		get f() {
			return this.#f;
		}

		set f(f) {
			this.#f = f;
			this.#c = (f!! - 32) * (5 / 9);
		}
	}

	const temperature = new Temperature();
</script>

<main class="h-screen">
	<section
		class="container mx-auto mt-24 max-w-xl rounded-md border border-black bg-gray-200 p-4 drop-shadow-md"
	>
		<div class="max-w- flex flex-col border">
			<h2 class="font-semibold">Temperature Converter</h2>
			<div class="my-10 flex gap-4 text-nowrap drop-shadow-xl">
				<input
					bind:value={temperature.c}
					class="max-w-32 rounded border pl-1"
					name="celcius"
					id="celcius"
					type="text"
				/>
				<label class="font-semibold" for="celcius">Celsius =</label>
				<input
					bind:value={temperature.f}
					class="max-w-32 rounded border pl-1"
					name="fahrenheit"
					id="fahrenheit"
					type="text"
				/>
				<label class="font-semibold" for="fahrenheit">Fahrenheit</label>
			</div>

			<a class="max-w-16 rounded bg-white p-2 font-semibold text-black" href="/">Home</a>
		</div>
	</section>
</main>
