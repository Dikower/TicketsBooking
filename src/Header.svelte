<script>
    import { slide } from 'svelte/transition';
    import {getContext} from 'svelte'
    let detailed_filter = false;
    export let genres;
    export let chosen_genre = genres[0];
</script>
<div class="component">
    <div class="filter" on:click={() => detailed_filter === true ? detailed_filter = false : detailed_filter = true}>
    <p class="chosen_genre">{chosen_genre}</p>
    <div class="filter_button">
    <svg width=16 height=16>
                <line x1=2 y1=2 x2=8 y2=8></line>
                <line x1=8 y1=8 x2=14 y2=2></line>
            </svg>
</div>

</div>
</div>
<div class="flex_box">
 {#if detailed_filter === true}
<div class="all_genres" transition:slide|local>
    {#each genres as genre}
        {#if chosen_genre !== genre}
    <div class="genre" on:click={() => {chosen_genre = genre; detailed_filter=false}}>{genre}</div>
            {/if}
        {/each}

</div>
{/if}
</div>
<style>
    @media all and (max-width: 510px) {
        .all_genres {
            display: grid;
            grid-template-columns: 1fr 1fr;
        }
        .flex_box {
            justify-content: center;
        }
    }
    @media all and (min-width: 510px) {
        .all_genres {
            display: flex;
        flex-wrap: wrap;
        justify-content: left;
        }
        .flex_box {
            justify-content: left;
        }
    }
    .component {
        width: 100%;
        height: 55px;
        font-family: var(--main-font);
        color: var(--text-cyan);
        font-size: 30px;
        z-index: 20;
    }
    .filter {
        width: 230px;
        height: 100%;
        display: inline-flex;
        align-items: center;
    }
    .filter:hover {
        cursor: pointer;
    }
    .chosen_genre {
        margin: 20px 0 0 15px;
    }
    .filter_button {
        width: 16px;
        height: 16px;
        margin-left: 10px;
        margin-top: 5px;
    }
    line {
        color: var(--text-cyan);
        stroke: currentColor;
        stroke-width: 2;
    }
    .flex_box {
        width: 100%;
        display: flex;
    }
    .all_genres {
        margin-top: 20px;
        background-color: var(--most-dark-color);
        font-size: 20px;
        padding: 0 0 10px 5px;
        border-radius: 20px;
    }
    .genre {
        text-align: center;
        margin: 15px 10px 5px 15px;
        font-family: var(--main-font);
        color: var(--text-blue-light);
        font-size: 0.9em;
        border: 2px solid var(--blue);
        border-radius: 20px;
        padding: 5px 15px;
    }
    .genre:hover {
        color: var(--text-cyan);
        cursor: pointer;
    }
</style>