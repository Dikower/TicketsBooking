
<script>
	import Card from './Card.svelte';
	import {onMount} from 'svelte'

	let screenWidth;
	let films = [
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
			['Паразиты', 'posters/parasites.jpg', 'Описание фильма', ['Драма', 'Триллер', 'Комедия'], 8.3],
	];

</script>
<svelte:window bind:innerWidth={screenWidth}/>

<main>
	<section style="--columns-amount: {Math.floor((screenWidth - 30) / 225)}">
		{#each films as film}
			<Card title="{film[0]}" poster_path="{film[1]}" description="{film[2]}" tags="{film[3]}" mark="{film[4]}"/>
		{/each}
	</section>
</main>


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
		--cyan: #81F7E5;
		--text-cyan: #C5FBF3;
		--text-cyan-p: #ECFEFB;
		--text-cyan-span: #87DEE8;

		--pink: #EF476F;

		--main-font: 'Roboto Condensed', sans-serif;

		background: var(--most-dark-color);
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
		gap: 20px 30px;
		height: 100%;
		width: 100%;
		margin: 40px;
	}
</style>