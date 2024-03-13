<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import Persona from './Persona.svelte';

	export let texto = '';

	let lineas = texto.split('\n');
	const escuadraNombre = lineas[0];
	let miembros = lineas.slice(1).map(linea => {
		let [rol, nombre] = linea.split('-');
		return { rol: rol.trim(),
				 nombre: nombre.trim() };
	});
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
