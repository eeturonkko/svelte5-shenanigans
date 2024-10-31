<script lang="ts">
	let length = $state(0);
	let password = $state('');

	function generatePassword() {
		password = '';
		const charset =
			'abcdefghijklmnopqrstuvwxyzåäöABCDEFGHIJKLMNOPQRSTUVWXYZ^ÄÖ0123456789!@#$%^&*()_+';
		for (let i = 0; i < length; i++) {
			password += charset.charAt(Math.floor(Math.random() * charset.length));
		}
		return password;
	}
</script>

<main class="h-screen">
	<section
		class="container mx-auto mt-24 max-w-xl rounded-md border border-black bg-gray-200 p-4 drop-shadow-md"
	>
		<div class="max-w- flex flex-col border">
			<h2 class="mb-2 font-semibold">Password Generator</h2>
			<input bind:value={length} type="range" min="0" max="24" class="max-w-xs" />
			<p class="font-semibold">Password length: {length}</p>

			<button class="my-4 max-w-24 rounded bg-white px-5 font-semibold" onclick={generatePassword}
				>Generate</button
			>
		</div>

		<div class="mb-4">
			{#if password.length > 0}
				<p class="font-semibold">Generated password: <span class="font-medium">{password}</span></p>
			{/if}
		</div>
		<a class="max-w-16 rounded bg-white p-2 font-semibold text-black" href="/">Home</a>
	</section>
</main>
