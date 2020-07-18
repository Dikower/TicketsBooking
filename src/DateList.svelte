<script>
    import {getContext} from 'svelte'

    export let chosen = undefined;
    let page = 0;
    let data = getContext('film_info');
    let schedule = data['schedule'];

    function changePage(value) {
        let new_page = page + value;
        if (new_page < schedule.length && new_page >= 0) {
            page = new_page;
        }
    }
</script>


<div class="page-block">
    <button type="button" class="arrow leftArrow" class:hidden={page === 0} on:click={() => changePage(-1)}>
        <svg width=17 height=17>
            <line x1=0 y1=9 x2=10 y2=0></line>
            <line x1=0 y1=9 x2=10 y2=17></line>
        </svg>
    </button>
    <div class="sessions-block">
        <h2 class="date">{schedule[page][0]}</h2>
        {#each schedule[page][1] as session}
            <button class="time-button" type="button" on:click={() => chosen = [schedule[page][0], session]}>{session}</button>
        {/each}
    </div>
    <button type="button" class="arrow rightArrow" class:hidden={page === schedule.length-1}
            on:click={() => changePage(+1)}>
        <svg width=17 height=17>
            <line x1=17 y1=9 x2=7 y2=0></line>
            <line x1=17 y1=9 x2=7 y2=17></line>
        </svg>
    </button>
</div>

<style>
    @media all and (max-width: 700px) {
        .page-block {
            margin: 50px 0 30px 0;
        }
    }
    .hidden {
        opacity: 0
    }

    .date {
        font-family: var(--main-font);
        font-size: 2em;
        color: var(--text-blue-span);
    }

    .page-block {
        /*height: 100%;*/
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    .sessions-block {
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .time-button {
        font-family: var(--main-font);
        color: var(--text-blue-light);
        font-weight: 700;
        font-size: 1.3em;
        border: 2px solid transparent;
        border-radius: 20px;
        padding: 5px 15px;
    }

    .time-button:hover {
        border-color: var(--blue);
    }

    .arrow {
        border-radius: 30px;
        width: 50px;
        height: 50px;
        margin-top: 20px;
    }

    .leftArrow {
        padding-left: 10px;
    }

    .rightArrow {
        padding-right: 10px;
    }

    .arrow:hover line {
        color: var(--cyan);
    }

    .arrow:active line {
        color: var(--blue);
    }

    .arrow:active {
        background: var(--most-dark-color);
    }

    line {
        color: var(--text-cyan-p);
        stroke: currentColor;
        transition: all .5s ease;
    }
</style>