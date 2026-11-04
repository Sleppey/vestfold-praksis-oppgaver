<script lang="ts">

async function fetchNrkData() {
    try {
        const response = await fetch("https://psapi.nrk.no/channels/p3musikk/liveelements");
        if (!response.ok) {
            throw new Error(`Response status: ${response.status}`);
        }

        return await response.json();
    } catch (error) {
        console.error((error as Error).message);
        return [];
    }
};

async function getData() {

    const data = await fetchNrkData();
    const recentSong = data[data.length -1];
    const title = recentSong.title;
    const artist = recentSong.description;
    const albumCover = recentSong.imageUrl;
    const type = recentSong.type;
    
    console.log("| Title:", title,"| Artist:", artist,"| CoverURL:", albumCover, "| Type:", type);
};

getData();

</script>

<h1>Gleep glorp</h1>
<p>goomy</p>
