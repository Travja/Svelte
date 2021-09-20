<script>
    import Bug from './modules/Bug.svelte';
    import BugListItem from './modules/BugListItem.svelte';
    import Card from './modules/Card.svelte';
    import ThemeSwitcher from './modules/ThemeSwitcher.svelte';

    let bugObjs = [];

    let bugs = [
        {
            status: "confirmed",
            title: "This is a bug",
            description: "Hey.. this doesnt work. I've tried everything but I can't get it to go anywhere. Help me! If I keep typing a really long thing, will it solve my problems? If I pester, does it work?"
        },
        {title: "This is bug 2", status: "rejected"},
        {title: "This is bug 3", status: "inprogress", comments: ["Comment one", "Comment two.. this works."]},
        {key: 3}
    ];

    const cards = [
        {src: "https://analyticsindiamag.com/wp-content/uploads/2020/10/7d744a684fe03ebc7e8de545f97739dd.jpg"},
        {src: "https://thumbs.dreamstime.com/b/rainbow-love-heart-background-red-wood-60045149.jpg"},
        {src: "https://lh3.googleusercontent.com/proxy/VBLCheaRpLRIAqSfSgwP2eeXXBmfGCcwwoA-lecEX5QdXsToZ-k5AwFA9I9MzI_9cO2tQaiFnYQDyYMp0Ymxy6VwD175_oxjMkEQPHNSw1iQSJpNH43_8cydIa1sSzmvqy4r_NVRfbLcHJoe96x2HjbwiAuE"}
    ];

    let list;
    let bugElm;
    let activeIndex;
    const clickBug = (e) => {
        console.log(e.detail);
        let idx = e.detail.index;

        if (bugElm && activeIndex !== idx) {
            bugElm.addEventListener('outroend', () => showBug(bugs[idx]));
            closeBug();
        } else showBug(bugs[idx]);
        activeIndex = idx;
    };

    const closeBug = () => {
        openBug = undefined;
        bugElm = undefined;
    };

    let openBug;
    const showBug = (bug) => {
        openBug = bug;
    };
</script>

<ThemeSwitcher/>
<h3>Bugs</h3>
<ul bind:this={list}>
    {#each bugs as bug, i}
        <BugListItem {...bug} index={i} on:click={clickBug}/>
    {/each}
</ul>
<div class="wrapper">
    {#each cards as card}
        <Card {...card}/>
    {/each}
</div>

{#if openBug}
    <Bug class="modal" bind:this={bugElm}
         {...openBug}
         on:close={closeBug}/>
{/if}

<style>
    .wrapper {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }
</style>