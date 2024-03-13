<script>
	import * as Card from '$lib/components/ui/card/index.js';
	import Separator from '$lib/components/ui/separator/separator.svelte';
	import Button from '$lib/components/ui/button/button.svelte';
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

<Card.Root class="w-[700px]">
	<Card.Header>
		<Card.Title>Alpha 1-1</Card.Title>
	</Card.Header>
	<Separator class="mb-5" />
	<Card.Content>
		<div
			class="flex items-center"
			class:bg-red-300={esRojo}
			class:bg-blue-300={esAzul}
			class:bg-yellow-300={esOro}
			class:bg-green-300={esVerde}
		>
			<p class="mr-24">1. snakemarenostrum</p>
			<div>
				<Button class="w-24 bg-red-500" on:click={setRojo}>Rojo</Button>
				<Button class="w-24 bg-blue-500" on:click={setAzul}>Azul</Button>
				<Button class="w-24 bg-yellow-500" on:click={setOro}>Oro</Button>
				<Button class="w-24 bg-green-500" on:click={setVerde}>Verde</Button>
			</div>
		</div>
		<Separator class="my-5" />
		<div class="flex items-center">
			<p class="mr-24">1. snakemarenostrum</p>
			<div>
				<Button class="w-24 bg-red-500">Rojo</Button>
				<Button class="w-24 bg-blue-500">Azul</Button>
				<Button class="w-24 bg-yellow-500">Oro</Button>
				<Button class="w-24 bg-green-500">Verde</Button>
			</div>
		</div>
		<Separator class="my-5" />
		<div class="flex items-center">
			<p class="mr-24">1. snakemarenostrum</p>
			<div>
				<Button class="w-24 bg-red-500">Rojo</Button>
				<Button class="w-24 bg-blue-500">Azul</Button>
				<Button class="w-24 bg-yellow-500">Oro</Button>
				<Button class="w-24 bg-green-500">Verde</Button>
			</div>
		</div>
		<Separator class="my-5" />
	</Card.Content>
</Card.Root>
