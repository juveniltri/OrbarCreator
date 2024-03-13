<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import Persona from './Persona.svelte';

	const escuadra = `RACOON 1-2
Líder de Equipo (R12)-Diablo
Fusilero (R12)-Aguja
Fusilero (R12)-Rylod
Fusilero AT (R12)-Fernanrl
Sanitario (R12)-JMartin`;
	const escuadraNombre = 'RACOON 1-2';
</script>

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>{escuadraNombre}</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content>
		<ol class="list-decimal">
			<Persona nombre="Proplayer" rol="Medico" />
			<Persona nombre="Proplayer" rol="Medico" />
		</ol>
	</Card.Content>
</Card.Root>
