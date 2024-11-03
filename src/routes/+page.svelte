<script lang="ts">
	import { onMount } from 'svelte';
	import { themeChange } from 'theme-change';
    import autoAnimate from '@formkit/auto-animate';

	let todos = $state<string[]>([]);
	let newTodo = $state('');

	function addTodo() {
		if (newTodo.trim()) {
			todos = [...todos, newTodo.trim()];
			newTodo = '';
		}
	}

	function removeTodo(index: number) {
		todos = todos.filter((_, i) => i !== index);
	}

	onMount(() => {
		themeChange(false);
	});
</script>

<div class="container mx-auto p-4 max-w-2xl">
	<h1 class="text-3xl font-bold mb-6">Todo App</h1>

	<!-- Theme selector -->
	<div class="mb-6">
		<select data-choose-theme class="select select-bordered w-full max-w-xs">
			<option value="">Default</option>
			<option value="light">Light</option>
			<option value="dark">Dark</option>
			<option value="cupcake">Cupcake</option>
			<option value="bumblebee">Bumblebee</option>
			<option value="emerald">Emerald</option>
			<option value="corporate">Corporate</option>
			<option value="synthwave">Synthwave</option>
			<option value="retro">Retro</option>
			<option value="cyberpunk">Cyberpunk</option>
			<option value="valentine">Valentine</option>
			<option value="halloween">Halloween</option>
			<option value="garden">Garden</option>
			<option value="forest">Forest</option>
			<option value="aqua">Aqua</option>
			<option value="lofi">Lofi</option>
			<option value="pastel">Pastel</option>
			<option value="fantasy">Fantasy</option>
			<option value="wireframe">Wireframe</option>
			<option value="black">Black</option>
			<option value="luxury">Luxury</option>
			<option value="dracula">Dracula</option>
			<option value="cmyk">Cmyk</option>
			<option value="autumn">Autumn</option>
			<option value="business">Business</option>
			<option value="acid">Acid</option>
			<option value="lemonade">Lemonade</option>
			<option value="night">Night</option>
			<option value="coffee">Coffee</option>
			<option value="winter">Winter</option>
			<option value="dim">Dim</option>
			<option value="nord">Nord</option>
			<option value="sunset">Sunset</option>
		</select>
	</div>

	<!-- Todo input -->
	<div class="join w-full">
		<input
			type="text"
			bind:value={newTodo}
			placeholder="Add a new todo"
			class="input input-bordered join-item flex-1"
			onkeydown={(e) => e.key === 'Enter' && addTodo()}
		/>
		<button class="btn btn-primary join-item" onclick={addTodo}>Add</button>
	</div>

	<!-- Todo list -->
	<div class="mt-6">
		{#if todos.length === 0}
			<div class="text-center py-4 bg-base-200 rounded-lg">
				<span class="text-base-200/60">No todos yet. Add one above!</span>
			</div>
		{:else}
			<ul use:autoAnimate class="space-y-2">
				{#each todos as todo, index}
					<li class="flex items-center justify-between p-3 bg-base-200 rounded-lg">
						<span>{todo}</span>
						<button 
							class="btn btn-ghost btn-sm btn-circle"
							onclick={() => removeTodo(index)}
						>
							✕
						</button>
					</li>
				{/each}
			</ul>
		{/if}
	</div>
</div>
