<script>
    let show = false
    let handleClick = ()=>{
        show = !show
    }
</script>

<div class="main-button">
    <button on:click={handleClick}>Instructions</button>
</div>

<div class="container {`show-${show}`}">
    <button class="close-button" on:click={handleClick}>X</button>
  <h3>Instructions</h3>

  <p>Welcome you Beatmaker!</p>
  
  <p>
    You can click or touch the pads to play the instruments. These pads can also be triggered by
    using the number keys on your keyboard 1-9 (including the numpad).
  </p>
  <p>
    Below the pads is a sequencer made up of blocks which allows you to create a looping beat. The
    blue light indicates when block is currently being played in the loop. You can click on the
    blocks to activate the coresponding instrument in that spot, when activated it turns orange. 
  </p>
  <p>There is a mute button under the logo that silences all the audio</p>
  <p>The Tempo slider allows you to control the speed of the loop</p>
  <p>Hope you enjoy!</p>
  
</div>


<style scoped>
    button{
        background-color: white;
    border-radius: 5px;
    border: 1px solid orange;
  }
  .close-button{
      position: absolute;
      right: 10px;
  }
    .container{
        
        position: fixed;
        z-index: 500;
        width: 300px;
        padding: 10px;
        background-color: rgb(255, 255, 255);
        color: rgb(230, 112, 2);
        border: 1px solid rgb(230, 112, 2);
        transition: all .5s;
        font-weight: 500;
        border-radius: 5px;
    }
    .main-button{
        position: fixed;
        width: 200px;
        right: -80px;
    }
    .show-true{
        right:10px;
    }
    .show-false{
        right: -400px;
    }
</style>

