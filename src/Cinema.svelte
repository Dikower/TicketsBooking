<script>
    import { setContext} from 'svelte'
    import { writable } from 'svelte/store'

    export let width = 10;
    export let height = 7;
    export let seatSize = 20;
    export let gridGap = 5;
    export let chosenSeats = [];

    let heightArray = Array.from(Array(height).keys());
    let widthArray = Array.from(Array(width).keys());

</script>

<div class="component" style="
    --width: {width}; --height: {height};
    --seatSize: {seatSize}px; --gridGap: {gridGap}px;">
    <p>Экран</p>
    <hr>
    <div class="grid">
        {#each heightArray as row}
            {#each widthArray as column}
                <label class="checkbox"><input type="checkbox" bind:group={chosenSeats} class="seat" value="{row},{column}"></label>
            {/each}
        {/each}
    </div>
</div>
<style>
    @media all and (max-width: 700px) {
        .component {
            --height-grid-px: calc(((var(--seatSize) + var(--gridGap)) * var(--height) + var(--gridGap)) * 0.75);
            --width--grid-px: calc(((var(--seatSize) + var(--gridGap)) * var(--width) - var(--gridGap)) * 0.75);
            width: var(--width--grid-px);
            height: var(--height--grid-px);
        }
        .grid {
            grid-template-rows: repeat(var(--height), calc(var(--seatSize) * 0.75));
            grid-template-columns: repeat(var(--width), calc(var(--seatSize) * 0.75));
            grid-gap: calc(var(--gridGap) * 0.8);
        }
        .checkbox > input {
            height: calc(var(--seatSize) * 0.75);
            width: calc(var(--seatSize) * 0.75);
        }
    }

    @media all and (min-width: 700px) {
        .component {
            --height-grid-px: calc((var(--seatSize) + var(--gridGap)) * var(--height) + var(--gridGap));
            --width--grid-px: calc((var(--seatSize) + var(--gridGap)) * var(--width) - var(--gridGap));
            width: var(--width--grid-px);
            height: var(--height--grid-px);
        }
        .grid {
            grid-template-rows: repeat(var(--height), var(--seatSize));
            grid-template-columns: repeat(var(--width), var(--seatSize));
            grid-gap: var(--gridGap);
        }
        .checkbox > input {
            height: var(--seatSize);
            width: var(--seatSize);
        }
        }

    .component {
        display: flex;
        justify-content: space-between;
        flex-direction: column;
        background: var(--most-dark-color);
        padding: 20px;
        border-radius: 20px;
    }

    hr {
        /*width: var(--width--grid-px);*/
        margin-bottom: 30px;
        width: 100%;
        color: var(--text-cyan-p);
    }

    .grid {
        display: grid;
    }

    .checkbox {
        display: inline-flex;
        cursor: pointer;
        position: relative;
    }

    .checkbox > input {
        -webkit-appearance: none;
        -moz-appearance: none;
        -o-appearance: none;
        appearance: none;
        border: 1px solid var(--text-cyan-span);
        border-radius: 4px;
        outline: none;
        transition-duration: 0.3s;
        background-color: var(--less-dark-color);
        cursor: pointer;
    }

    .checkbox > input:checked {
        border: 1px solid var(--less-dark-color);
        background-color: var(--text-cyan-span);
    }

    p {
        color: var(--text-cyan-p);
        margin: 0;
        padding: 0;
        font-family: var(--main-font-family);
        text-align: center;
    }
</style>
