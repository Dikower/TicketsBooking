<script>
    import {getContext} from 'svelte'

    const {poster_path, title, tags, mark, schedule, description} = getContext('film_info')

    var detailed_store = getContext('detailed_store');
    let handleClick = () => detailed_store.set(true);
    let hovered = false
</script>

<div class="card" class:hovered on:click={handleClick}>
    <!--on:hover content-->
    <div class="poster-block">
        <!--        {#if hovered}-->
        <!--            <div transition:fade class="hover-info-block">-->
        <!--                <h1 class="available-sessions-title">Доступные сеансы</h1>-->
        <!--                <div class="page-block">-->
        <!--                    <button class="arrow" class:hidden={page === 0} on:click={() => changePage(-1)}>-->
        <!--                        <svg width=17 height=17>-->
        <!--                            <line x1=0 y1=9 x2=10 y2=0></line>-->
        <!--                            <line x1=0 y1=9 x2=10 y2=17></line>-->
        <!--                        </svg>-->
        <!--                    </button>-->
        <!--                    <div class="sessions-block">-->
        <!--                        <h2 class="date">{schedule[page][0]}</h2>-->
        <!--                        {#each schedule[page][1] as session}-->
        <!--                            <button class="time-button" on:click={enter_detailed}>{session}</button>-->
        <!--                        {/each}-->
        <!--                    </div>-->
        <!--                    <button class="arrow" class:hidden={page === schedule.length-1} on:click={() => changePage(+1)}>-->
        <!--                        <svg width=17 height=17>-->
        <!--                            <line x1=17 y1=9 x2=7 y2=0></line>-->
        <!--                            <line x1=17 y1=9 x2=7 y2=17></line>-->
        <!--                        </svg>-->
        <!--                    </button>-->
        <!--                </div>-->
        <!--            </div>-->
        <!--        {/if}-->
        <img class:hovered class="poster" alt="Постер" src="{poster_path}">
    </div>
    <!--end of hover content-->

    <div class="title-mark-block">
        <h1 class="title">{title}</h1>
        <div class="mark">
            <h1 class="mark">{mark}</h1>
            <img class="star" alt="*" src="star.svg" type="svg">
        </div>
    </div>
    <div class="tags-block">
        {#each tags as tag}
            <span class="tag">{tag}</span>
        {/each}
    </div>
</div>

<style>
    .poster {
        width: 100%;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
        transition: filter 0.5s ease;
    }

    .poster.hovered {
        filter: blur(1px);
    }

    .poster-block {
        margin: 0;
        padding: 0;
        display: flex;
    }

    .card {
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

    .card.hovered {
        box-shadow: 0 0 20px 10px var(--most-dark-color-shadow);
    }

    .title-mark-block {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        width: calc(100% - 20px);
        margin: 10px 0 0 10px;
    }

    .title {
        font-family: var(--main-font);
        color: var(--text-cyan);
        font-size: 1.1em;
        font-weight: 500;
        text-align: justify;
    }

    .tags-block {
        margin-left: 10px;
    }

    .tag {
        margin-right: 4px;
        font-size: 0.8em;
        color: var(--text-blue-span);
    }

    .mark {
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

    .hover-info-block {
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