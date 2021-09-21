<script>
    import DiscordButton from './DiscordButton.svelte';
</script>

<footer>
    <hr>
    <div class="links">
        <a href="#">Contact Me!</a>
        <DiscordButton fontSize="1"/>
    </div>
    <div class="copy">&copy; 2021 Travja</div>
</footer>

<style>
    .links {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .links > * {
        margin: 10px;
        padding: 10px;
        border-radius: 6px;
        background-color: rgba(0, 0, 0, .3);
        display: flex;
        align-items: center;
    }

    a {
        color: var(--fg-color);
    }

    a:hover {
        text-decoration: none;
    }

    .copy {
        text-align: center;
        font-size: 0.9em;
    }
</style>