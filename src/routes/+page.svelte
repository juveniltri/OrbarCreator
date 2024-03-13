<script>
	import CartaOrbat from '../components/CartaOrbat.svelte';
	let textoEscuadra = '';
	let escuadras = [];

	function generarCartas() {
		escuadras = textoEscuadra
			.trim()
			.split('\n\n')
			.map((escuadras) => {
				return escuadras.trim();
			});
	}
</script>

<textarea bind:value={textoEscuadra} class="h-32 w-full p-2" />

<div class="m-2 flex space-x-2">
	<button
		on:click={generarCartas}
		class="rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700"
	>
		Generar Carta
	</button>
	<button
		on:click={() => {
			textoEscuadra = '';
		}}
		class="rounded bg-gray-500 px-4 py-2 font-bold text-white hover:bg-gray-700"
	>
		Limpiar
	</button>
</div>

{#if escuadras.length > 0}
	<div class="mx-2 grid grid-cols-3 gap-y-3">
		{#each escuadras as equipoTexto (equipoTexto)}
			<CartaOrbat {equipoTexto}></CartaOrbat>
		{/each}
	</div>
{/if}

<style>
</style>
