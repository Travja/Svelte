<svelte:options accessors/>
<script>
    import CloseButton from './CloseButton.svelte';
    import {createEventDispatcher} from 'svelte';
    import {fly} from 'svelte/transition';

    export let status = "Unconfirmed";
    export let title = "Untitled";
    export let description = "No description.";
    export let comments = [];
    export let key = {};

    let desc;
    let isFocused = false;

    const editDescription = () => {
        desc.contentEditable = true;
        desc.focus();
        isFocused = true;
    };

    const loseFocus = () => {
        desc.contentEditable = false;
        console.log(description);
        isFocused = false;
    };

    export const addComment = (comment) => {
        comments = [...comments, comment];
    };

    let block;
    export const addEventListener = (evt, callback) => {
        block.addEventListener(evt, callback);
    };

    const dispatch = createEventDispatcher();
    const closeClicked = () => {
        dispatch('close', {});
    };

</script>

<div class="bug"
     bind:this={block}
     in:fly={{ x: -200, duration: 500 }} out:fly={{ x: -200, duration: 250 }}>
    <CloseButton on:click={closeClicked}/>
    <div class="content">
        <div class="centered">
            <h3>{title}</h3>
            <hr>
            <div class="desc">
                <div class="edit" on:click={editDescription}>Edit</div>
                <div on:blur={loseFocus}
                     contenteditable="false"
                     bind:this={desc}
                     bind:textContent={description}></div>
            </div>
            <hr>
        </div>
        {#if comments && comments.length > 0}
            <h4>Comments</h4>
            {#each comments as comment}
                <div>{comment}</div>
            {/each}
        {:else}
            <div class="comment">
                <div>No comments... Be the first!</div>
            </div>
        {/if}
    </div>
</div>

<style>
    .bug {
        position: relative;
        margin: 20px;
        padding: 20px;
        min-width: 200px;
        max-width: 500px;
        background-color: rgba(0, 0, 0, 0.2);
        border-radius: 10px;
        box-shadow: 5px 5px 10px #000;
    }

    .content {
        position: relative;
        display: flex;
        flex-direction: column;
    }

    h3 {
        margin: 0;
    }

    .centered {
        text-align: center;
    }

    .desc {
        position: relative;
    }

    hr {
        margin: 12px 0;
        border-color: var(--fg-color);
        transition: border;
        transition-duration: .3s;
        transition-timing-function: ease-in-out;
    }

    .edit {
        float: right;
        /*position: absolute;*/
        /*top: 0;*/
        /*right: 20px;*/
        color: var(--link-color);
        text-decoration: underline;

        transition-property: color, text-shadow, background-color;
        transition-duration: .3s;
        transition-timing-function: ease-in-out;
    }

    .edit:hover {
        cursor: pointer;
    }

    .comment {
        display: flex;
        flex-grow: 1;
        align-items: flex-end;
        justify-content: center;
    }
</style>