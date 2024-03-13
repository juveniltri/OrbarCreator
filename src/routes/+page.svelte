<script>
	import CartaOrbat from '../components/CartaOrbat.svelte';
	let textoEscuadra = '';
	let mostrarCarta = false;
</script>

<textarea bind:value={textoEscuadra} class="w-full h-32 p-2"/>

<div class="flex space-x-2 mt-2">
    <button on:click={() => { mostrarCarta = true; }} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Generar Carta
    </button>
    <button on:click={() => { textoEscuadra = ''; mostrarCarta = false; }} class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
        Limpiar
    </button>
</div>

{#if mostrarCarta }
<div class="p-5">
	<CartaOrbat texto={textoEscuadra}></CartaOrbat>
</div>
{/if}
<style>
</style>
