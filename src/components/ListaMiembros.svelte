<script>
	import Button from '$lib/components/ui/button/button.svelte';
	import Separator from '$lib/components/ui/separator/separator.svelte';

	import { flip } from 'svelte/animate';
	import { createEventDispatcher } from 'svelte';

	export let miembros;

	let isOver = false;

	let colorSeleccionado = {};
	function setColor(color, index) {
		colorSeleccionado[index] = colorSeleccionado[index] === color ? '' : color;
	}

	const dispatch = createEventDispatcher();

	function getDraggedParent(node) {
		if (!node.dataset.index) {
			return getDraggedParent(node.parentNode);
		} else {
			return { ...node.dataset };
		}
	}

	function onDragStart(e) {
		const dragged = getDraggedParent(e.target);
		e.dataTransfer?.setData('source', dragged?.index.toString());
	}

	function onDragOver(e) {
		const id = e.target.dataset?.id;
		const dragged = getDraggedParent(e.target);
		isOver = dragged?.id ?? false;
	}

	function onDragLeave(e) {
		const dragged = getDraggedParent(e.target);
		isOver === dragged.id && (isOver = false);
	}

	function onDrop(e) {
		isOver = false;
		const dragged = getDraggedParent(e.target);
		reorder({
			from: e.dataTransfer?.getData('source'),
			to: dragged.index
		});
	}

	const reorder = ({ from, to }) => {
		const newList = [...miembros];
		newList[from] = [newList[to], (newList[to] = newList[from])][0];

		dispatch('sort', newList);
	};
</script>

<ol class="list-decimal">
	{#each miembros as miembro, index (miembro.id)}
		<li
			class="transition-all"
			class:over={miembro.id === isOver}
			data-index={index}
			data-id={miembro.id}
			draggable="true"
			on:dragstart={onDragStart}
			on:dragover|preventDefault={onDragOver}
			on:dragleave={onDragLeave}
			on:drop|preventDefault={onDrop}
			animate:flip={{ duration: 300 }}
		>
			<div
				class="flex items-center"
				class:bg-red-300={colorSeleccionado[index] === 'rojo'}
				class:bg-blue-300={colorSeleccionado[index] === 'azul'}
				class:bg-yellow-300={colorSeleccionado[index] === 'oro'}
				class:bg-green-300={colorSeleccionado[index] === 'verde'}
			>
				<div class="min-w-80">
					<p class="mr-24">{miembro.rol}: <br />{miembro.nombre}</p>
				</div>
				<div class="flex gap-3">
					<Button class="w-4/12 bg-red-500" on:click={() => setColor('rojo', index)}>Rojo</Button>
					<Button class="w-4/12 bg-blue-500" on:click={() => setColor('azul', index)}>Azul</Button>
					<Button class="w-4/12 bg-yellow-500" on:click={() => setColor('oro', index)}>Oro</Button>
					<Button class="w-4/12 bg-green-500" on:click={() => setColor('verde', index)}
						>Verde</Button
					>
				</div>
			</div>
			<Separator class="my-5" />
		</li>
	{/each}
</ol>

<style>
	.over {
		@apply scale-105 border-gray-400;
	}
</style>
