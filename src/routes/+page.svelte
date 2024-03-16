<script>
	import { onMount } from 'svelte';
	import CartaOrbat from '../components/CartaOrbat.svelte';
	import Notificaciones from '../components/Notificaciones.svelte';

	let textoEscuadra = '';
	let escuadras = [];
	let mostrarNotificacion = false;

	function convertirTextoAEscuadras(texto) {
		const bloquesEquipo = texto.trim().split('\n\n');
		const escuadras = bloquesEquipo.map((bloque) => {
			const lineas = bloque.split('\n');
			const nombre = lineas[0];
			const players = lineas.slice(1);
			return {
				name: nombre,
				players: players
			};
		});

		return escuadras;
	}

	function generarCartas() {
		if (textoEscuadra.trim() === '') {
			mostrarNotificacion = true;
			setTimeout(() => (mostrarNotificacion = false), 3000);
		} else {
			escuadras = convertirTextoAEscuadras(textoEscuadra);
			localStorage.setItem('escuadras', JSON.stringify(escuadras));
			mostrarNotificacion = false;
		}
	}

	onMount(() => {
		const cacheEscuadras = localStorage.getItem('escuadras');
		if (cacheEscuadras) {
			escuadras = JSON.parse(cacheEscuadras);
		}
	});

	function borrarCache() {
		localStorage.removeItem('escuadras');
		escuadras = [];
	}
</script>

<div class="flex items-start justify-center mt-8">
    <div class="flex flex-col w-[50%]">
        <textarea bind:value={textoEscuadra} class="h-32 w-full p-2"></textarea>

        <div class="flex flex-column justify-end gap-2">
            <button
                on:click={generarCartas}
                class="rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700"
            >
                Generar Carta
            </button>
            <button
                on:click={borrarCache}
                class="rounded bg-gray-500 px-4 py-2 font-bold text-white hover:bg-gray-700"
            >
                Borrar cache
            </button>
        </div>
    </div>
</div>

{#if mostrarNotificacion}
    <Notificaciones message="Tienes que rellenar la info del orbat en el cuadro de texto" type="error"></Notificaciones>
{/if}

{#if escuadras.length > 0}
    <div class="grid grid-cols-2 gap-8">
        {#each escuadras as equipoTexto (equipoTexto.name)}
            <CartaOrbat {equipoTexto}></CartaOrbat>
        {/each}
    </div>
{/if}

<style>
    textarea {
        margin: 0 auto;
    }

    .mt-8 {
        margin-top: 2rem;
    }
</style>

<!--
<div class="textarea">
	<textarea bind:value={textoEscuadra} class="h-32 p-2" />
	
	<button
		on:click={generarCartas}
		class="rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700"
	>
		Generar Carta
	</button>
	<button
		on:click={borrarCache}
		class="rounded bg-gray-500 px-4 py-2 font-bold text-white hover:bg-gray-700"
	>
		Borrar cache
	</button>
</div>

{#if mostrarNotificacion}
	<Notificaciones message="Tienes que rellenar la info del orbat en el cuadro de texto" type="error"
	></Notificaciones>
{/if}

{#if escuadras.length > 0}
	<div class="mx-2 grid grid-cols-2 gap-y-3">
		{#each escuadras as equipoTexto (equipoTexto.name)}
			<CartaOrbat {equipoTexto}></CartaOrbat>
		{/each}
	</div>
{/if}
-->