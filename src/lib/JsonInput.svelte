<script lang="ts">
  import { jsonData } from "./store";
</script>

<div class="area-wrapper">
  <textarea bind:value={$jsonData} />
</div>

<style>
  .area-wrapper {
    height: 100%;
    display: grid;
    place-items: center;
  }
  textarea {
    height: 90%;
    width: 90%;
  }
</style>