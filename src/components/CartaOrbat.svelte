<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import Persona from './Persona.svelte';

	export let equipoTexto = '';

	const escuadraNombre = equipoTexto.name;
	let miembros =  equipoTexto.players.map((player, index) => {
		let [rol, nombre] = player.split('-').map( part => part.trim());
		return { rol, nombre, id: index };
	});

	function handleDragStart(event, id) {
		console.log("Estamos en Drag");
        event.dataTransfer.setData('application/json', JSON.stringify({ id }));
    }

    function handleDragOver(event) {
        event.preventDefault();
    }

    function handleDrop(event) {
        event.preventDefault();
        const data = JSON.parse(event.dataTransfer.getData('application/json'));
		const nombre = data.nombre;
    }
</script>

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>{escuadraNombre}</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content on:dragover={handleDragOver}
				  on:drop={handleDrop}>
		<ol class="list-decimal">
			{#each miembros as {nombre, rol, id} (id)}
				<Persona {nombre} {rol} {id}
						on:dragstart={event => handleDragStart(event, id)}/>
			{/each}
		</ol>
	</Card.Content>
</Card.Root>
