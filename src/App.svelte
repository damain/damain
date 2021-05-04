<script>
  import {onMount} from 'svelte'
  import Instructions from "./Instructions.svelte"
  import MuteIcon from './MuteIcon.svelte'
  import Pads from "./Pads.svelte";
  import Sequence from "./Sequence.svelte";
  
  let interval 
  let pads = [
    { name: "claves", file: "./sounds/perc-808.wav", image:"./images/claves.png", code: "7", sequence:[] },
    { name: "clap", file: "./sounds/clap-808.wav", image:"./images/clap.png", code: "8", sequence:[] },
    { name: "crash", file: "./sounds/crash-808.wav", image:"./images/crash.png", code: "9", sequence:[] },
    { name: "toms", file: "./sounds/tom-808.wav", code: "4", image:"./images/toms.png", sequence:[] },
    { name: "cowbell", file: "./sounds/cowbell-808.wav", image:"./images/cowbell.png", code: "5", sequence:[] },
    { name: "kick", file: "./sounds/kick-808.wav", image:"./images/kick.png", code: "6", sequence:[] },

    { name: "snare", file: "./sounds/snare-808.wav", image:"./images/snare.png", code: "1", sequence:[] },
    { name: "closedHat", file: "./sounds/hihat-808.wav", image:"./images/closedHat.png", code: "2", sequence:[] },
    { name: "openedHat", file: "./sounds/openhat-808.wav", image:"./images/openedHat.png", code: "3", sequence:[] },
  ];
  let beat = 0
  let bpm =60
  $: bps = Math.floor((1000 / (bpm/60))/4)
  
  let muted = false
  let oldbps = 0
  let tick = ()=>{
    if (oldbps != bps){
      oldbps = bps
      clearInterval(interval)
      interval = setInterval(tick, bps)
    }

	  if (beat < 15){
		  beat +=1
	  }else{
		  beat = 0
	  }
  }
  
  onMount(()=>{
    interval  = setInterval(tick, bps)
  })
  
  let handleSequenceChanged = (data, i)=>{
	  pads[i].sequence = data.detail
  }

  let toggleMute = ()=>{
	  muted = !muted
  }
</script>

<main>
  <Instructions></Instructions>
	<div class="inline-block"><img class="logo" src="./images/logo.png" alt=""></div>
  <div><button class="mute" on:click={toggleMute}>
    <MuteIcon muted={muted} />
  </button>
    <div class="inline-block tempo">
      Tempo 
      <div class="inline-block">
        <div class="bpm">{bpm} </div>
        <button on:click={()=>{bpm--}} >-</button><input bind:value={bpm} type="range" min="40" max="218"><button on:click={()=>{bpm++}}>+</button>
      </div>
    </div>
  </div>
  <Pads pads={pads} beat={beat} settings={{muted}}></Pads>
  <div id="sequencer">
	  {#each pads as instrument, i}
      <div class="instName"><span class="nameContainer">{instrument.name} </span><img class="icon" src={instrument.image} alt=""></div>
      <Sequence pad={instrument} beat={beat} on:sequenceChanged={(data)=>{handleSequenceChanged(data, i)}} ></Sequence>
    {/each}
  </div>
</main>

<style>
  button{
    border-radius: 5px;
    border: 1px solid orange;
  }
  main{
    font-family: 'Oxygen', sans-serif;
  }
  .instName{
    display: inline;
    height: 30px;
    line-height: 30px;
    text-transform: capitalize;
    border-bottom: 1px dashed orange;
    padding-left: 3px;
    overflow: hidden;

  }
  .nameContainer{
    overflow-x: hidden;
  }
  #sequencer{
    padding-top: 30px;
    display: grid;
    gap: 3px;
    grid-template-columns: 1fr 11fr;
    vertical-align: middle;
    line-height: 30px;
  }
  .inline-block{
    display: inline-block;
  }
  .bpm{
    text-align: center;
    position: relative;
    top:13px;
    color: orange;
  }
  .tempo button, .tempo input{
    background-color: transparent;
    border: none;
    padding:5px;
    color: orange;
    line-height: 20px;
    height: 20px;
    font-size: 30px;
    margin-bottom:0px;
    font-weight:bold;
  }
  .tempo button{
    padding-left: 5px;
    padding-right:5px;
  }
  .mute{
    width: 80px;
    margin-right: 10px;
    background-color: transparent;
  }
  .logo{
    height: 50px;
  }
  .icon{
        height: 20px;
      
    }

</style>
