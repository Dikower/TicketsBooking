<svelte:head>
    <title>Бронирование билета</title>
</svelte:head>

<script>
    import Card from './Card.svelte';
    import Header from './Header.svelte';
    let chosen_genre;
    let screenWidth;
    let genres = [
        'Все фильмы', 'Драма', 'Триллер', 'Комедия', 'Ужастик', 'Детектив', 'Боевик', 'Фэнтези', 'Мюзикл', 'Фантастика', 'Мультфильм'
    ];
    let counter = 1;
    let films = [
        ['Паразиты', 'posters/parasites.jpg', '', ['Драма', 'Триллер', 'Комедия'], 8.3],
        ['Pulp fiction', 'posters/pulp_fiction.jpg', '', ['Боевик', 'Триллер', 'Комедия'], 10],
        ['Mad Max', 'posters/mad_max.jpg', '', ['Боевик'], 7],
        ['Kill Bill', 'posters/Kill_Bill.jpg', '', ['Боевик', 'Триллер',], 9],
        ['Довод', 'posters/Tenet.jpg', '', ['Боевик', 'Триллер'], '???'],
        ['Прочь', 'posters/Get_out.jpg', '', ['Ужастик', 'Триллер', ''], 8.6],
        ['Джокер', 'posters/Joker.jpg', '', ['Триллер', 'Комедия', 'Драма'], 8.5],
        ['Олдбой', 'posters/Oldboy.jpg', '', ['Детектив', 'Триллер'], 7.5],
    ];
</script>
<svelte:window bind:innerWidth={screenWidth}/>
<body>
<main>
    <Header genres={genres} bind:chosen_genre={chosen_genre}/>
    <section style="--columns-amount: {Math.floor((Math.min(screenWidth, 1440) - 30) / 325)}">
        {#each films as film}
            {#if chosen_genre === 'Все фильмы' || film[3].indexOf(chosen_genre) !== -1}
            <Card title="{film[0]}" poster_path="{film[1]}" description="{film[2]}" tags="{film[3]}" mark="{film[4]}" chosen_genre="{chosen_genre}"/>
                {/if}
        {/each}
    </section>
</main>
</body>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@300;400;700&display=swap');

    :root {
        --most-dark-color: #191C24;
        --most-dark-color-shadow: #121417;
        --normal-dark-color: #24272B;
        --normal-dark-color-shadow: #1A1C1F;
        --less-dark-color: #35393C;

        --yellow: #FFCF00;
        --blue: #5C95FF;
        --text-blue-span: #ADCAFF;
        --text-blue-light: #D6E4FF;
        --blue-dark: #1F6DFF;

        --cyan: #81F7E5;
        --text-cyan: #C5FBF3;
        --text-cyan-p: #ECFEFB;
        --text-cyan-span: #87DEE8;

        --pink: #EF436B;
        --pink-dark: #E11444;
        --pink-light: #F0567A;
        --pink-lighter: #F47C98;

        --main-font: 'Roboto Condensed', sans-serif;
        background: var(--most-dark-color);

    }

    @media screen and (min-width: 720px) {
        body::-webkit-scrollbar {
            width: 7px; /* width of the entire scrollbar */
        }

        body::-webkit-scrollbar-track {
            background: transparent; /* color of the tracking area */
        }

        body::-webkit-scrollbar-thumb {
            background-color: var(--pink); /* color of the scroll thumb */
            border-radius: 20px; /* roundness of the scroll thumb */
            border: 3px solid var(--pink); /* creates padding around scroll thumb */
        }

        body {
            overflow-y: scroll;
            scrollbar-width: thin; /* "auto" or "thin"  */
            scrollbar-color: var(--pink) transparent; /* scroll thumb & track */
            scroll-bar-border: 30px;
            padding: 0;
        }
    }

    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        max-width: 1440px;
        margin: 0 auto;
    }


    section {
        display: grid;
        /*align-items: center;*/
        justify-items: center;
        grid-template-columns: repeat(var(--columns-amount), 1fr);
        gap: 30px 20px;
        height: 100%;
        width: 100%;
        margin: 20px 40px;
    }
.invisible {
    display: none;
}
    .error_message {
        color: var(--text-cyan-p);
        font-size: 25px;
        text-align: center;
    }
</style>