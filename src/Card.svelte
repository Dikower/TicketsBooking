<script>
    import {fade} from 'svelte/transition'

    export let poster_path = './';
    export let title = 'Loreum';
    export let description = 'Loreum ipsum';
    let detailed = true;

    let card;
    let background;


    function handleBackgroundClick(event){
        if (event.target === background) {
            detailed = false;
        }
    }

    function enter_detailed(event){
        detailed = true;
    }
</script>


<div class="component" on:click={() => detailed = true}>
    <img class="preview_poster" alt="Постер" src="{poster_path}">
    <h1 class="card-title">{title}</h1>
</div>

{#if detailed}
    <div bind:this={background} class="background" transition:fade on:click={handleBackgroundClick}>
        <div bind:this={card} class="detailed-card">
            <div class="content">
                <img class="poster" alt="Постер" src="{poster_path}">
                <h1 class="detailed-card-title">{title}</h1>
                <p>{description}</p>
            </div>
            <button class="cancel-button" on:click={() => detailed = false}>
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
        position: absolute;
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

    .detailed-card {
        width: 90%;
        max-width: 1150px;
        height: 500px;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 5px var(--normal-dark-color-shadow);
        z-index: 21;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .cancel-button {
        width: 32px;
        height: 32px;
        background: inherit;
        border: none;
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
    }
    .detailed-card-title {
        font-size: 3em;
        font-family: var(--main-font);
        font-weight: 500;
        margin: 30px 0 0 30px;
        color: var(--text-cyan);
    }



    .preview_poster {
        width: 100%;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
    }

    .component {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        width: 200px;
        height: 345px;
        transition: color 0.5s ease, width 0.5s ease, height 0.5s ease;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 1px var(--most-dark-color-shadow);
        border-radius: 10px;
    }

    .card-title {
        font-size: 0.98em;
        font-family: var(--main-font);
        font-weight: 500;
        padding: 10px;
        margin: 0;
        color: var(--text-cyan);
    }

</style>