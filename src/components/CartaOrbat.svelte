<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import Persona from './Persona.svelte';

	export let equipoTexto = '';

	console.log(equipoTexto.name);

	const escuadraNombre = equipoTexto.name;
	let miembros =  equipoTexto.players.map(player => {
		let [rol, nombre] = player.split('-').map( part => part.trim());
		return { rol, nombre };
	});

	console.dir(miembros);
</script>

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>{escuadraNombre}</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content>
		<ol class="list-decimal">
			{#each miembros as {nombre, rol}}
				<Persona {nombre} {rol}/>
			{/each}
		</ol>
	</Card.Content>
</Card.Root>
