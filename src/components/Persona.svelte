<script>
	import Button from '$lib/components/ui/button/button.svelte';
	import Separator from '$lib/components/ui/separator/separator.svelte';

	export let nombre;
	export let rol;

	let esRojo = false;
	let esAzul = false;
	let esOro = false;
	let esVerde = false;
	function setRojo(event) {
		esAzul = false;
		esVerde = false;
		esOro = false;
		esRojo = !esRojo;
	}
	function setAzul(event) {
		esRojo = false;
		esVerde = false;
		esOro = false;
		esAzul = !esAzul;
	}
	function setOro(event) {
		esRojo = false;
		esVerde = false;
		esAzul = false;
		esOro = !esOro;
	}
	function setVerde(event) {
		esRojo = false;
		esOro = false;
		esAzul = false;
		esVerde = !esVerde;
	}
</script>

<div
	class="flex items-center"
	class:bg-red-300={esRojo}
	class:bg-blue-300={esAzul}
	class:bg-yellow-300={esOro}
	class:bg-green-300={esVerde}
>
	<p class="mr-24">1. {rol}: {nombre}</p>
	<div>
		<Button class="w-24 bg-red-500" on:click={setRojo}>Rojo</Button>
		<Button class="w-24 bg-blue-500" on:click={setAzul}>Azul</Button>
		<Button class="w-24 bg-yellow-500" on:click={setOro}>Oro</Button>
		<Button class="w-24 bg-green-500" on:click={setVerde}>Verde</Button>
	</div>
</div>
<Separator class="my-5" />
