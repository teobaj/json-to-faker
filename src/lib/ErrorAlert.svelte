<script lang="ts">
  import { error } from './store';
  let show:boolean = true;

  $: show = !!$error
</script>

{#if show}
  <div class="alert">
    <div class="wrapper">
      <h3>Error:</h3>
      <button on:click={() => {show = false}}>Close</button>
    </div>
    <span>{$error}</span>
  </div>
{/if}

<style>
  .alert {
    position: absolute;
    right: 40px;
    bottom: 40px;
    border: 2px solid #f50b65;
    background: #e76094;
    padding: 1rem;
    border-radius: 10px;
    max-width: 500px;
  }
  .wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.25rem;
  }
  h3 {
    margin: 0
  }
</style>