<script>
    import {fade} from 'svelte/transition'

    export let poster_path = './';
    export let title = 'Loreum';
    export let description = 'Loreum ipsum';
    export let tags = ['Loreum', 'ipsum'];
    export let mark = 9.7;

    let detailed = false;

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


<div class="preview-card" on:click={() => detailed = true}>
    <img class="preview_poster" alt="Постер" src="{poster_path}">
    <div class="preview-title-mark-block">
        <h1 class="preview-title">{title}</h1>
        <div class="preview-mark">
            <h1 class="mark">{mark}</h1>
            <img class="star" alt="*" src="star.svg" type="svg">
        </div>
    </div>
    <div class="preview-tags-block">
        {#each tags as tag}
            <span class="preview-tag">{tag}</span>
        {/each}
    </div>
</div>

{#if detailed}
    <div bind:this={background} class="background" transition:fade on:click={handleBackgroundClick}>
        <div bind:this={card} class="detailed-card">
            <div class="content">
                <img class="poster" alt="Постер" src="{poster_path}">
                <div class="text-block">
                    <h1 class="detailed-title">{title}</h1>
                    <p class="detailed-description">{description}</p>
                </div>
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
    h1 {
        margin: 0;
        padding: 0;
    }
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
        border-radius: 10px;
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
        border-bottom-left-radius: 10px;
        border-top-left-radius: 10px;
    }

    .text-block {
        display: flex;
        flex-direction: column;
        margin: 30px 0 0 30px;
        height: 100%;
    }

    .detailed-title {
        font-size: 3em;
        font-family: var(--main-font);
        font-weight: 500;
        padding: 0;
        margin: 0;
        color: var(--text-cyan);
    }

    .detailed-description {
        height: 100px;
        font-size: 1em;
        color: var(--text-cyan-p);
        /*text-align: justify;*/
        text-overflow: ellipsis;
    }



    .preview_poster {
        width: 100%;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
    }

    .preview-card {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        width: 200px;
        height: 360px;
        transition: color 0.5s ease, width 0.5s ease, height 0.5s ease;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 1px var(--most-dark-color-shadow);
        border-radius: 10px;
    }
    .preview-title-mark-block {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        width: calc(100% - 20px);
        margin: 10px 0 0 10px;

    }
    .preview-title {
        font-family: var(--main-font);
        color: var(--text-cyan);
        font-size: 1.1em;
        font-weight: 500;
        text-align: justify;
    }
    .preview-tags-block{
        margin-left: 10px;

    }
    .preview-tag {
        margin-right: 4px;
        font-size: 0.8em;
        color: var(--text-blue-span);
    }
    .preview-mark {
        width: 50px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-around;
    }
    .star {
        width: 20px;
        height: 20px;
    }
    .mark {
        font-size: 1em;
        color: var(--cyan);
        font-weight: 500;
    }


</style>