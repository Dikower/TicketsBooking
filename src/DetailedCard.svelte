<script>
    import { getContext } from 'svelte'
    import { fade } from 'svelte/transition'
    import Form from './Form.svelte'

    const {poster_path, title, tags, mark, schedule, description} = getContext('film_info');
    let detailed_store = getContext('detailed_store');
    let background;
</script>

{#if $detailed_store}
<div bind:this={background} class="background" transition:fade
     on:click={(event) => event.target === background ? detailed_store.set(false) : undefined}>

    <div class="card">
        <div class="content">
            <img class="poster" alt="Постер" src="{poster_path}">
            <Form/>
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
    @media all and (max-width: 700px) {
        .card {
            display: flex;
            flex-direction: row;
            height: 520px;
            margin-top: 30px;
            padding-top: 10px;
        }
        .content {
            width: 100%;
        }
    }
    @media all and (max-width: 880px) {
        .poster {
            display: none;
        }
        .card {
            width: 80%;
        }
    }
    @media all and (max-width: 980px) and (min-width: 880px){
    .card {
        width: 100%;
    }
    }
    @media all and (min-width: 980px) {
        .card {
            width: 90%;
        }
    }
    @media all and (min-width: 700px) {
        .card {
            display: flex;
        flex-direction: row;
        justify-content: space-between;
            height: 500px;
        }
    }
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
        max-width: 1000px;
        min-width: 300px;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 5px var(--normal-dark-color-shadow);
        z-index: 21;
        border-radius: 10px;
    }

    .cancel-button {
        width: 32px;
        height: 32px;
        margin-top: 5px;
        margin-right: 5px;
        /*top: 0;*/
        /*right: 0;*/
    }
    .cancel-button:hover {
        cursor: pointer;
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
        justify-content: space-between;
        align-items: center;
        width: 95%;
    }

    .poster {
        /*top: 0;*/
        width: auto;
        height: 100%;
        align-self: flex-start;
        border-bottom-left-radius: 10px;
        border-top-left-radius: 10px;
    }
</style>