<script lang="ts">

async function fetchNrkData() {
    try {
        const response = await fetch("https://psapi.nrk.no/channels/p3musikk/liveelements");
        if (!response.ok) {
            throw new Error(`Response status: ${response.status}`);
        }

        const result = await response.json();
        return result;
    } catch (error) {
        console.error((error as Error).message);
        return [];
    }
}

async function getdata() {

    const data = await fetchNrkData();
    const datasize = data.length;
    const recentsong = data[datasize -1]
    const title = recentsong.title
    const artist = recentsong.description
    const albumcover = recentsong.imageUrl
    const type = recentsong.type
    
    console.log("| Title:", title,"| Artist:", artist,"| CoverURL:", albumcover, "| Type:", type)
    
}

getdata()

</script>

<h1>Gleep glorp</h1>
<p>goomy</p>
