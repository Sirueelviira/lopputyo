<script>
  export let fakta;
  export let nimi;
  import { createEventDispatcher } from 'svelte';
		const dispatch = createEventDispatcher();

  function suljeIkkuna() {
    dispatch('suljeIkkuna')
  }
</script>


  <div class="modal">
    <div class="modal-content">
      <p>Tänään {nimi} oppii kissoista seuraavaa:</p>
      <slot></slot>
      <p>{fakta}</p>
      <button on:click={suljeIkkuna}>SULJE</button>
    </div>
  </div>


<style>

/* Jarkon koodia tehtävästä 17 */

	.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

.modal {
  padding: 3rem;
  position: fixed;
  top: 10vh;
  left: 8vw;
  width: 80%;
  max-height: 80vh;
  background: #466568;
  border-radius: px;
  z-index: 100;
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.26);
  overflow: scroll;
}

</style>