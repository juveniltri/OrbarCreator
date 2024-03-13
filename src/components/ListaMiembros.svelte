<script>
	import Button from '$lib/components/ui/button/button.svelte';
	import Separator from '$lib/components/ui/separator/separator.svelte';

	export let miembros;

	let colorSeleccionado = {};
	function setColor(color, index) {
		colorSeleccionado[index] = colorSeleccionado[index] === color ? '' : color;
	}
</script>

<ol>
	{#each miembros as miembro, index (miembro.id)}
		<li>
			<div
				class="flex items-center"
				class:bg-red-300={colorSeleccionado[index] === 'rojo'}
				class:bg-blue-300={colorSeleccionado[index] === 'azul'}
				class:bg-yellow-300={colorSeleccionado[index] === 'oro'}
				class:bg-green-300={colorSeleccionado[index] === 'verde'}
			>
				<p class="mr-24">{miembro.rol}: {miembro.nombre}</p>
				<div>
					<Button class="w-24 bg-red-500" on:click={() => setColor('rojo', index)}>Rojo</Button>
					<Button class="w-24 bg-blue-500" on:click={() => setColor('azul', index)}>Azul</Button>
					<Button class="w-24 bg-yellow-500" on:click={() => setColor('oro', index)}>Oro</Button>
					<Button class="w-24 bg-green-500" on:click={() => setColor('verde', index)}>Verde</Button>
				</div>
			</div>
		</li>
		<Separator class="my-5" />
	{/each}
</ol>
