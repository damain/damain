<script>
  import Light from "./Light.svelte";
  import {createEventDispatcher} from "svelte"
  export let pad = {};
  export let beat = 0;
  let dispatch = createEventDispatcher()
  let positions = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0];

let handleClick= (data)=>{
    console.log(data)
    let i = data.detail.index
    positions[i] = positions[i] ? 0: 1
    dispatch("sequenceChanged", positions)
}
</script>
<div class="row">
  <div class="sequence">
    {#each positions as position, i}
      <Light name={pad.name} lit="{position}" beat={beat} index={i} on:lightClicked= {handleClick}></Light>
    {/each}
  </div>
</div>


<style>
    .sequence{
        /* padding-top: 10px; */
        display:grid;
        gap: 3px;
        grid-template-columns: 1fr 1fr 1fr 1fr  1fr 1fr 1fr 1fr  1fr 1fr 1fr 1fr  1fr 1fr 1fr 1fr;
    }
    .row{
      display: inline;
      width: 100%
    }
</style>
