<script>
    import {getContext} from 'svelte'
    import {fade} from 'svelte/transition'

    const {poster_path, title, tags, mark, schedule, description} = getContext('film_info')

    var detailed_store = getContext('detailed_store');
    let handleClick = () => detailed_store.set(true);

    let hovered = false;
</script>

<div class="card" class:hovered
     on:click={handleClick}
     on:mouseenter={() => hovered = true}
     on:mouseleave={() => hovered = false}>
    <img class:hovered class="poster" alt="Постер" src="{poster_path}">

    <!--on:hover content-->
    {#if hovered}
        <div class="info-block" transition:fade>
            <div class="first-row">
                <h1 class="title">{title}</h1>
                <div class="mark">
                    <h1 class="mark">{mark}</h1>
                    <img class="star" alt="*" src="star.svg" type="svg">
                </div>
            </div>
            <span class="tags">{tags.join(', ')}</span>
            <p class="description">{description}</p>
        </div>
    {/if}

</div>

<style>
    .poster {
        width: 100%;
        border-radius: 5px;
        transition: filter 0.5s ease;
    }

    .poster.hovered {
        filter: blur(1px);
    }

    .card {
        --card-width: 300px;
        --card-height: 429px;

        display: flex;
        flex-direction: column;
        align-items: flex-start;
        width: var(--card-width);
        height: auto;
        transition: all 0.5s ease;
        background: var(--normal-dark-color);
        box-shadow: 0 0 20px 1px var(--most-dark-color-shadow);
        border-radius: 10px;
        margin: 1px;
        cursor: pointer;
    }

    .card.hovered {
        box-shadow: 0 0 20px 10px var(--most-dark-color-shadow);
    }


    .title {
        font-family: var(--main-font);
        color: var(--text-cyan);
        font-size: 2em;
        font-weight: 500;
        text-align: justify;
        margin-right: 20px;
    }

    .tags {
        margin-right: 4px;
        font-size: 1.2em;
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
        width: 1em;
        height: 1em;
    }

    .mark {
        font-size: 1.3em;
        color: var(--pink);
        font-weight: 500;
    }

    .first-row {
        display: flex;
        flex-direction: row;
        justify-content: center;
        width: 80%;
    }

    .description {
        margin: 0 auto;
        color: var(--text-cyan-p);
        overflow: hidden;
        width: 80%;
        text-align: justify;
        max-height: 16em;
    }

    .info-block {
        z-index: 10;
        position: absolute;
        width: var(--card-width);
        height: var(--card-height);
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background: rgba(0, 0, 0, 0.6);
        border-radius: 5px;
    }

</style>