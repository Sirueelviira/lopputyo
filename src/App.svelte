<script>
	export let name;
  import { onMount } from 'svelte';
	import Modal from './Modal.svelte';
	
	
	let showModal = false;
	let nimi = '';

	function openModal() {
    showModal = true;
  }

	function closeModal() {
		showModal = false;
		console.log('test')
	}

	
  let kissafaktoja = '';
	onMount(async () => {
    const response = await fetch("https://meowfacts.herokuapp.com/");
    if (!response.ok) {
      throw new Error('cannot fetch the data');
    }
    kissafaktoja = await response.json();
		
  });

	const errorIlmoitus = "Nimi täytyy syöttää!";
  let nimiVierailtu = false;
  $: nimiOk = nimi.length > 1 || !nimiVierailtu;

	
</script>

<main>


	<h1>{name}</h1>
	<p>Syötä nimesi:</p>
	<div class='syotanimi'><input bind:value={nimi}  on:blur={() => (nimiVierailtu=true) } ></div>
	{#if !nimiOk}
	<p class="errori">{errorIlmoitus}</p>
	{/if}
	<button disabled={!nimiOk} on:click={() => showModal = true}>Avaa</button>

	<img src="./kuvia/kissa.jpg" alt="emt"/>

  <header>
    <slot name="header" />
	
		{#if showModal}
	 <Modal on:suljeIkkuna={closeModal} nimi={nimi} fakta={kissafaktoja.data}></Modal>
		{/if}
  </header>

  <footer>
    <slot name="footer" />
  </footer>

	
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background-color: rgb(164, 177, 189);
	}


	h1 {
		color: #638e93;
		font-family: "Lucida Console", "Courier New", monospace;
		text-transform: uppercase;
		font-size: 5em;
		font-weight: 150;
	}

	.syotanimi {
		padding-right: 4px;
		border-radius: 3px;
	}

	img {
		display: block;
    margin-left: auto;
  	margin-right: auto;
		margin-top: 10px;
 	  width: 50%;
	}

	.errori {
		color: red;
	
	}


	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>