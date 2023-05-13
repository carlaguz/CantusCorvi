<script>
  let index = 0;
  export const tracks = [{title:"", url:""}];
  let track = tracks[index].url;
  let player = new Audio();
  let isPlaying = false;

  let progress = 0;
  // @ts-ignore
  let interval = null;
  let playIcon = "/assets/play-solid.svg";

  const togglePlay = () => {
    if (isPlaying) {
      player.pause();
      //@ts-ignore
      clearInterval(interval);
      playIcon = "/assets/play-solid.svg";
    } else {
      player.play();
      playIcon = "/assets/pause-solid.svg";
      interval = setInterval(() => {
        progress = player.currentTime;
      }, 500);
    }

    isPlaying = !isPlaying;
  };
</script>

<section>
  <audio bind:this={player}>
    <source src={track} type="audio/mpeg" />
  </audio>
  <input type="range" bind:value={progress} min="0" max={player.duration} />
  <div>
    <button><img src="/assets/backward-solid.svg" alt="Forward btn" /></button>
    <button style="height: 75px;width:75px" on:click={() => togglePlay()}>
      <img src={playIcon} alt="Forward btn" />
    </button>
    <button><img src="/assets/forward-solid.svg" alt="Forward btn" /></button>
  </div>
</section>

<style>
  section {
    display: grid;
    height: 80%;
    width: 80%;
    place-items: center;
    gap: 10px;
  }
  input[type="range"] {
    appearance: none;
    -webkit-appearance: none;
    width: 100%;
    height: 8px;
    border-radius: 4px;
    background: rgb(216, 112, 147);
    cursor: pointer;
  }
  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    background: #fff;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 5px solid pink;
  }
  div {
    width: 80%;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  button {
    background: #fff;
    border: none;
    height: 50px;
    width: 50px;
    border-radius: 50%;
    display: flex;
  }
  button img {
    margin: auto;
    height: 60%;
  }
</style>
