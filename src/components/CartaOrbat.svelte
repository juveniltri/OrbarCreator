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
</script>

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>{escuadraNombre}</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content>
		<ListaMiembros {miembros} on:sort={sortList} />
	</Card.Content>
</Card.Root>
