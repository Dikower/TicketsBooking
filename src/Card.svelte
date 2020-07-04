<script>
    import {fade, fly} from 'svelte/transition'
    import ListSchedule from './ListSchedule.svelte'

    export let poster_path = './';
    export let title = 'Loreum';
    export let description = 'Loreum ipsum';
    export let tags = ['Loreum', 'ipsum'];
    export let mark = 9.7;
    export let schedule = [
        ["1 июля", ['12:10', '17:30', '20:50']],
        ["2 июля", ['10:15', '16:35', '19:55']],
        ["3 июля", ['10:15', '16:35', '19:55']],
        ["4 июля", ['10:15', '16:35', '19:55']],
    ];
    let page = 0;
    let old_page = 0;
    let detailed = false;
    let hovered = false;
    let card;
    let background;


    function handleBackgroundClick(event) {
        if (event.target === background) {
            detailed = false;
        }
    }

    function enter_detailed(event) {
        detailed = true;
    }

    function changePage(value) {
        let new_value = page + value
        if (new_value >= 0 && new_value < schedule.length) {
            old_page = page;
            page = new_value;
        }

    }
</script>


<div class="preview-card" class:hovered on:click={enter_detailed}>

    <!--on:hover content-->
    <div class="preview-poster-block">
        {#if hovered}
            <div transition:fade class="preview-hover-info-block">
                <h1 class="available-sessions-title">Доступные сеансы</h1>
                <div class="page-block">
                    <button class="arrow" class:hidden={page === 0} on:click={() => changePage(-1)}>
                        <svg width=17 height=17>
                            <line x1=0 y1=9 x2=10 y2=0></line>
                            <line x1=0 y1=9 x2=10 y2=17></line>
                        </svg>
                    </button>
                    <div class="sessions-block">
                        <h2 class="date">{schedule[page][0]}</h2>
                        {#each schedule[page][1] as session}
                            <button class="time-button" on:click={enter_detailed}>{session}</button>
                        {/each}
                    </div>
                    <button class="arrow" class:hidden={page === schedule.length-1} on:click={() => changePage(+1)}>
                        <svg width=17 height=17>
                            <line x1=17 y1=9 x2=7 y2=0></line>
                            <line x1=17 y1=9 x2=7 y2=17></line>
                        </svg>
                    </button>
                </div>
            </div>
        {/if}
        <img class:hovered class="preview-poster" alt="Постер" src="{poster_path}">
    </div>
    <!--end of hover content-->

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
        font-family: var(--main-font);
    }
    button {
        background: transparent;
        border: none;
        transition: all 0.5s ease;
    }
    button:active{
        background: transparent;
    }

    .hidden {
        visibility: hidden;
    }

    /* Detailed card */

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


    /*Preview card*/

    .preview-poster {
        width: 100%;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
        transition: filter 0.5s ease;
    }

    .preview-poster.hovered {
        filter: blur(1px);
    }

    .preview-poster-block {
        margin: 0;
        padding: 0;
        display: flex;
    }

    .preview-card {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        width: 200px;
        height: 360px;
        transition: all 0.5s ease;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 1px var(--most-dark-color-shadow);
        border-radius: 10px;
    }

    .preview-card.hovered {
        box-shadow: 0 0 20px 10px var(--most-dark-color-shadow);
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

    .preview-tags-block {
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
        color: var(--pink);
        font-weight: 500;
    }

    /* Hover menu*/

    .preview-hover-info-block {
        z-index: 10;
        position: absolute;
        width: 200px;
        height: 300px;
        display: flex;
        flex-direction: column;
        /*justify-content: center;*/
        align-items: center;
        background: rgba(0, 0, 0, 0.6);
        border-radius: 5px;
    }

    .available-sessions-title {
        font-size: 1.4em;
        justify-self: flex-start;
        color: var(--text-cyan);
        margin-top: 20px;
    }

    .date {
        font-family: var(--main-font);
        font-size: 1.3em;
        color: var(--text-blue-span);
    }
    .page-block {
        width: 90%;
        height: 90%;
        display: flex;
        flex-direction: row;
        align-items: center;
    }
    .sessions-block {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .time-button {
        font-family: var(--main-font);
        color: var(--text-blue-light);
        font-weight: 700;
        border: 2px solid transparent;
        border-radius: 20px;
        padding: 5px 15px;
    }
    .time-button:hover {
        border-color: var(--blue);
    }
    .arrow {
        height: 50px;
        /*width: 40px;*/
    }

</style>