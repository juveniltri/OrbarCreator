<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import ListaMiembros from './ListaMiembros.svelte';
	import Notificaciones from '../components/Notificaciones.svelte';

	export let equipoTexto = '';

	let mostrarNotificacion = false;

	const escuadraNombre = equipoTexto.name;
	let miembros = equipoTexto.players.map((player, index) => {
		let [rol, nombre] = player.split('-').map((part) => part.trim());
		return { rol, nombre, id: index };
	});

	function sortList(e) {
		const newList = e.detail;
		miembros = newList;
	}

	function exportBBCode() {
		let bbCode = `[b]Equipo ${escuadraNombre}:[/b]\n[list=1]\n`;
		miembros.forEach((miembro) => {
			let colorBBCode = '';
			console.log(miembro.color);

			if (miembro.color === 'rojo') {
				colorBBCode = '[color=#FF0000]';
			} else if (miembro.color === 'azul') {
				colorBBCode = '[color=#0080FF]';
			} else if (miembro.color === 'verde') {
				colorBBCode = '[color=#008000]';
			} else if (miembro.color === 'oro') {
				colorBBCode = '[color=#FFBF00]';
			}

			bbCode += `[*]${colorBBCode}${miembro.nombre}${colorBBCode ? '[/color]' : ''}\n`;
		});

		bbCode += `[/list]\n`;
		navigator.clipboard
			.writeText(bbCode)
			.then(() => {
				console.log('BBCode copiado al portapapeles');
				mostrarNotificacion = true;
				setTimeout(() => (mostrarNotificacion = false), 3000);
			})
			.catch((err) => {
				console.error('Error al copiar al portapapeles:', err);
			});
	}
</script>

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>
			{escuadraNombre}
		</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content>
		<ListaMiembros {miembros} on:sort={sortList} />
	</Card.Content>
	<Separator class="mb-5" />
	<Card.Footer>
		<button
			on:click={exportBBCode}
			class="rounded bg-green-500 px-4 py-2 font-bold text-white hover:bg-green-700"
		>
			Exportar a BBCode
		</button>
	</Card.Footer>
</Card.Root>

{#if mostrarNotificacion}
	<Notificaciones message="Has copiado la escuadra al portapapeles en formato BBCode" type="info"
	></Notificaciones>
{/if}