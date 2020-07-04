<script>
    import { getContext } from 'svelte'
    import { fade, fly } from 'svelte/transition'
    const {poster_path, title, tags, mark, schedule, description} = getContext('film_info')
    var detailed_store = getContext('detailed_store');
    let background;
</script>

{#if $detailed_store}
<div bind:this={background} class="background" transition:fade
     on:click={(event) => event.target === background ? detailed_store.set(false) : undefined}>

    <div class="card">
        <div class="content">
            <img class="poster" alt="Постер" src="{poster_path}">
            <div class="text-block">
                <h1 class="title">{title}</h1>
                <p class="description">{description}</p>
            </div>
        </div>
        <button class="cancel-button" on:click={() => detailed_store.set(false)}>
            <svg width=16 height=16>
                <line x1=2 y1=2 x2=14 y2=14></line>
                <line x1=2 y1=14 x2=14 y2=2></line>
            </svg>
        </button>
    </div>
</div>
{/if}

<style>
    .background {
        position: fixed;
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.7);
        z-index: 20;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .card {
        width: 90%;
        max-width: 1150px;
        height: 500px;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 5px var(--normal-dark-color-shadow);
        z-index: 21;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        border-radius: 10px;
    }

    .cancel-button {
        width: 32px;
        height: 32px;
        margin-top: 5px;
        margin-right: 5px;
    }

    .cancel-button:active {
        background: inherit;
    }

    line {
        color: var(--text-cyan);
        stroke: currentColor;
        stroke-width: 2;
    }

    .content {
        display: flex;
        flex-direction: row;
        justify-self: flex-start;
        width: 90%;
    }

    .poster {
        /*top: 0;*/
        width: auto;
        height: 100%;
        align-self: flex-start;
        border-bottom-left-radius: 10px;
        border-top-left-radius: 10px;
    }

    .text-block {
        display: flex;
        flex-direction: column;
        margin: 30px 0 0 30px;
        height: 100%;
    }

    .title {
        font-size: 3em;
        font-weight: 500;
        padding: 0;
        margin: 0;
        color: var(--text-cyan);
    }

    .description {
        height: 100px;
        font-size: 1em;
        color: var(--text-cyan-p);
        text-overflow: ellipsis;
    }
</style>