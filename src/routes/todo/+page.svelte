<script lang="ts">
	type TodoItem = {
		id: number;
		title: string;
		completed: boolean;
	};
	class TodoList {
		#todos = $state<TodoItem[]>([
			{
				id: 1,
				title: 'Learn SvelteKit',
				completed: false
			},
			{
				id: 2,
				title: 'Learn TailwindCSS',
				completed: false
			},
			{
				id: 3,
				title: 'Learn TypeScript',
				completed: false
			}
		]);

		get todos() {
			return this.#todos;
		}

		set Todo(title: string) {
			this.#todos = [
				...this.#todos,
				{
					id: this.#todos.length + 1,
					title,
					completed: false
				}
			];
		}
	}

	let todoText = $state<string>('');

	const addTodo = () => {
		todoList.Todo = todoText;
		todoText = '';
	};

	const todoList = new TodoList();
</script>

<main class="h-screen">
	<section
		class="container mx-auto mt-24 max-w-xl rounded-md border border-black bg-gray-200 p-4 drop-shadow-md"
	>
		<div class="max-w- flex flex-col border">
			<h2 class="mb-2 font-semibold">Todo app</h2>
			<div class="mb-4 flex flex-col gap-1">
				<label for="">Todo Text</label>
				<input bind:value={todoText} type="text" />
				<button onclick={addTodo}>Add todo</button>
				{#each todoList.todos as todo (todo.id)}
					<div class="flex justify-between">
						<p class="font-semibold">{todo.title}</p>
						<p>completed: {todo.completed}</p>
						<input type="checkbox" checked={todo.completed} />
					</div>
				{/each}
				<a class="max-w-16 rounded bg-white p-2 font-semibold text-black" href="/">Home</a>
			</div>
		</div>
	</section>
</main>
