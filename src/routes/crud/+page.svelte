<script lang="ts">
	type Person = {
		firstName: string;
		lastName: string;
	};

	let people = $state<Person[]>([
		{
			firstName: 'Eetu',
			lastName: 'Rönkkö'
		},
		{
			firstName: 'Inga ',
			lastName: 'Myllymäki'
		},
		{
			firstName: 'Loki',
			lastName: 'Kissa'
		},
		{
			firstName: 'Muuk',
			lastName: 'Kissa'
		}
	]);

	let selected = $state<Person>();
	let person = $state({ firstName: '', lastName: '' });
	let prefix = $state('');
	const filteredPeople = $derived(
		prefix ? people.filter((p) => p.lastName.toLowerCase().startsWith(prefix)) : people
	);

	$effect(() => {
		person = {
			firstName: selected?.firstName ?? '',
			lastName: selected?.lastName ?? ''
		};
	});

	function clearInput() {
		person = { firstName: '', lastName: '' };
	}

	function createPerson() {
		people.push(person);
		clearInput();
	}

	function UpdatePerson() {
		const index = people.findIndex((p) => p === selected);
		people[index] = person;
		clearInput();
	}

	function deletePerson() {
		const index = people.findIndex((p) => p === selected);
		people.splice(index, 1);
		clearInput();
	}
</script>

<main class="h-screen">
	<section
		class="container mx-auto mt-24 max-w-xl rounded-md border border-black bg-gray-200 p-4 drop-shadow-md"
	>
		<div class="max-w- flex flex-col border">
			<h2 class="font-semibold">Crud</h2>

			<!--Filter section starts-->
			<div class="flex max-w-60 items-center gap-2">
				<label class="text-nowrap" for="">Filter prefix:</label>
				<input type="text" class="max-w-[152px]" bind:value={prefix} />
			</div>
			<!--Filter section ends-->

			<!--Name selection and input fields starts-->
			<div class="mt-4 flex justify-between gap-20 border">
				<!--Name selection starts-->
				<select
					bind:value={selected}
					name=""
					id=""
					size={people.length + 1}
					class="flex flex-1 items-center bg-white"
				>
					{#if people.length === 0}
						<option value="nope">No people</option>
					{:else}
						{#each filteredPeople as person}
							<option value={person}>{person.lastName}, {person.firstName}</option>
						{/each}
					{/if}
				</select>
				<!--Name selection ends-->

				<!--Input fields for first and last name-->
				<div class="mt-4 flex flex-col gap-2">
					<label for="firstName">First name</label>
					<input
						bind:value={person.firstName}
						type="text"
						id="firstName"
						class=" rounded-md border border-black p-2"
					/>
					<label for="lastName">Last name</label>
					<input
						bind:value={person.lastName}
						type="text"
						id="lastName"
						class=" rounded-md border border-black p-2"
					/>
				</div>
				<!--Input fields for first and last name ends-->
			</div>
			<!--Buttons for CRUD operations starts-->
			<div class="mt-4 flex justify-end gap-2">
				<button onclick={createPerson} class="rounded-md bg-blue-500 p-2 font-semibold text-white"
					>Create</button
				>
				<button onclick={UpdatePerson} class="rounded-md bg-green-500 p-2 font-semibold text-white"
					>Update</button
				>
				<button onclick={deletePerson} class="rounded-md bg-red-500 p-2 font-semibold text-white"
					>Delete</button
				>
			</div>
		</div>
		<a class="rounded bg-white p-2 font-semibold text-black" href="/">Home</a>
	</section>
</main>
