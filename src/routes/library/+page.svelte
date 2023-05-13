<script>
    import Album from "../../component/Album.svelte";
    const fetchalbums = async () => {
        const res = await fetch("/api/songs.json");
        const data = await res.json();
        return data;
    };
</script>

<h1>library here</h1>
<ul>
    {#await fetchalbums() then albums}
        {#each albums as album}
            <li>
                <Album artist={album.artist}
                cover={album.cover}
                title={album.album} />
            </li>
        {/each}
    {/await}
</ul>

<style>
    ul {
        display: grid;
        list-style: none;
        grid-template-columns: repeat(5, 1fr);
        gap: 15px;
        width: 95%;
        margin: auto;
    }
</style>
