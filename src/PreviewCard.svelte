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
    {#if hovered && document.documentElement.clientWidth > 980}
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

<style>
    @media all and (max-width: 980px) {
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
        margin-bottom: 10px;
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
    }
    @media all and (min-width: 980px) {
        .preview-title-mark-block {
            display: none;
        }
        .preview-tags-block {
            display: none;
        }
    }
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