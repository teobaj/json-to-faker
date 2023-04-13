<script lang="ts">
  import FakerOutput from "./lib/FakerOutput.svelte";
  import JsonInput from "./lib/JsonInput.svelte";
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import ErrorAlert from "./lib/ErrorAlert.svelte";

  const copyToClipboard = () => {
    window.postMessage('copyToClipboard')
  }

</script>

<main>
  <header> 
    <div style="display: flex; gap: 1rem; justify-content:center; align-items:center;">
      <h3>JSON to Faker</h3>
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </div>
  <button on:click={copyToClipboard}>Copy To ClipBoard</button>
  </header>
  <div class="content">
    <JsonInput />
    <FakerOutput />
  </div>
  <ErrorAlert></ErrorAlert>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    height: 100vh;
    gap: 1rem;
    width: 100%;
  }
  header {
    height: 48px;
    padding: 0.25rem;
    background-color: #710686;
    display: flex;
    justify-content: center;
    gap: 1rem;
  }
  .content {
    flex-grow: 2;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
</style>
