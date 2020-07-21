<script>
    import { setContext } from 'svelte'
    import {getContext} from 'svelte'
    import { writable } from 'svelte/store'
    import PreviewCard from './PreviewCard.svelte'
    import DetailedCard from './DetailedCard.svelte'
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

    setContext('film_info', {poster_path, title, tags, mark, schedule, description});
    setContext('detailed_store', writable(false));
</script>

<PreviewCard/>
<DetailedCard/>
<style>
    :global(h1) {
        margin: 0;
        padding: 0;
        font-family: var(--main-font);
    }
    :global(button) {
        background: transparent;
        border: none;
        transition: all 0.5s ease;
    }
</style>