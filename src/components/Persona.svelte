<script>
	import Button from '$lib/components/ui/button/button.svelte';
	import Separator from '$lib/components/ui/separator/separator.svelte';

	export let nombre;
	export let rol;

	let colorSeleccionado = '';
	function setColor(color) {
		colorSeleccionado = colorSeleccionado === color ? '' : color;
	}
</script>

<li>
	<div
		class="flex items-center"
		class:bg-red-300={colorSeleccionado === 'rojo'}
		class:bg-blue-300={colorSeleccionado === 'azul'}
		class:bg-yellow-300={colorSeleccionado === 'oro'}
		class:bg-green-300={colorSeleccionado === 'verde'}
	>
		<p class="mr-24">{rol}: {nombre}</p>
		<div>
			<Button class="w-24 bg-red-500" on:click={() => setColor('rojo')}>Rojo</Button>
			<Button class="w-24 bg-blue-500" on:click={() => setColor('azul')}>Azul</Button>
			<Button class="w-24 bg-yellow-500" on:click={() => setColor('oro')}>Oro</Button>
			<Button class="w-24 bg-green-500" on:click={() => setColor('verde')}>Verde</Button>
		</div>
	</div>
</li>
<Separator class="my-5" />
