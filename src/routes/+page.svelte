<script>
	import CartaOrbat from '../components/CartaOrbat.svelte';
	let textoEscuadra = '';
	let escuadras = [];

	function generarCartas() {
		escuadras = textoEscuadra.trim().split('\n\n').map(escuadras => {
			return escuadras.trim();
		});		
	}
</script>

<textarea bind:value={textoEscuadra} class="w-full h-32 p-2"/>

<div class="flex space-x-2 mt-2">
    <button on:click={generarCartas} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Generar Carta
    </button>
    <button on:click={() => { textoEscuadra = ''}} class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
        Limpiar
    </button>
</div>

{#if escuadras.length > 0}
	<div class="p-5">
		{#each escuadras as equipoTexto(equipoTexto)}
			<CartaOrbat {equipoTexto}></CartaOrbat>			
		{/each}
	</div>
{/if}
<style>
</style>
