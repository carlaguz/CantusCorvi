<script>
  import AudioControlls from "./AudioControlls.svelte";
  let fetchAlbums = async () => {
    const res = await fetch("/api/songs.json");
    const data = await res.json();
    console.log(data[8]);
    return data[8];
  };
</script>

<section>
  {#await fetchAlbums() then { cover, artist, album, list }}
    <img src={cover} alt="cover" />
    <div style="text-align: center;">
      <h2>{album}</h2>
      <h4><i>{artist}</i></h4>
    </div>
    <ul>
      {#each list as { title }, i}
        <li>{i + 1}. {title}</li>
      {/each}
    </ul>
    <AudioControlls tracks={list}/>
  {/await}
</section>

<style>
  section {
    background-color: rgba(216, 112, 147, 0.33);
    border-radius: 10px;
    width: 320px;
    height: 540px;
    display: grid;
    place-items: center;
    grid-template-rows: 200px 50px 180px 1fr;
    overflow: hidden;
  }
  img {
    height: 95%;
    border-radius: 50%;
  }
  ul {
    padding: 3px 0;
    width: 80%;
    height: 100%;
    list-style: none;
    overflow: auto;
    overflow-x: hidden;

    scrollbar-width: auto;
    scrollbar-color: #8f54a0;
  }
  li {
    font-size: 1.2em;
    user-select: none;
    padding: 2px;
  }
  li:hover {
    background-color: rgba(0, 0, 0, 0.2);
    cursor: pointer;
  }
  ul::-webkit-scrollbar {
    width: 5px;
  }

  ul::-webkit-scrollbar-track {
    background: rgba(0, 0, 0, 0.2);
  }

  ul::-webkit-scrollbar-thumb {
    background-color: #8f54a0;
    border-radius: 8px;
  }
</style>
