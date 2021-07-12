<script>
	
	import Modal from './Modal.svelte';
	let modal
	
	function openModal1(){
		modal.command('open','type1')
	}
	function openModal2(){
		modal.command('open','type2')
	}
	
</script>

<button on:click={openModal1}>OPEN MODAL 1</button>
<button on:click={openModal2}>OPEN MODAL 2</button>
<Modal bind:this={modal} />
<style>
	
</style>