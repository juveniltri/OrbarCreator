<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import ListaMiembros from './ListaMiembros.svelte';

	export let equipoTexto = '';

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
		miembros.forEach( miembro => {
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
		navigator.clipboard.writeText(bbCode).then(() => {
            console.log('BBCode copiado al portapapeles');
        }).catch(err => {
            console.error('Error al copiar al portapapeles:', err);
        });
	}
</script>

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>
			{escuadraNombre}
			<button 
				on:click={exportBBCode}
				class="bg-green-500 text-white px-4 py-2 rounded m-2"
			>
				Exportar a BBCode
			</button>
		</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content>
		<ListaMiembros {miembros} on:sort={sortList} />
	</Card.Content>
</Card.Root>