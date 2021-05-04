<script>
  import Pad from "./Pad.svelte";
  export let pads = []
  export let beat = 0
    export let settings = {muted:false}
</script>

<div class="container">
  <div class="display">
    {#each pads as pad}
        <Pad pad={pad} beat={beat} settings={settings}/>
    {/each}
  </div>
</div>

<style>
  .display {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 15px;
  }
</style>
