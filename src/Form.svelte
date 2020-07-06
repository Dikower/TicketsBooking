<script>

    import Cinema from './Cinema.svelte'
    import DateList from './DateList.svelte'
    import {getContext} from 'svelte'

    const {title} = getContext('film_info')

    function printForm() {
        console.log('Телефон:', phoneInput);
        console.log('ФИО:', nameInput);
    }

    let phoneInput = '';
    let nameInput = '';

    let smallerPhone = phoneInput !== '';
    let smallerName = nameInput !== '';


</script>


<div class="component">
<h1 class="title">{title}</h1>
<form>
    <div class="input-wrapper">

        <label><input bind:value={phoneInput} type="phone"
                      on:focus={() => smallerPhone = true}
                      on:blur={() => smallerPhone = phoneInput !== ''}>
            <span class:focus={smallerPhone}>Телефон</span></label>

        <label><input bind:value={nameInput} type="name"
                      on:focus={() => smallerName = true}
                      on:blur={() => smallerName = nameInput !== ''}>
            <span class:focus={smallerName}>ФИО</span></label>
        <button type="button" on:click={printForm}>Забронировать</button>
    </div>
    <!--    <Cinema/>-->
    <DateList/>


</form>
</div>

<style>
    .component {
        margin-left: 40px;
        display: flex;
        width: 100%;
        height: 90%;
        flex-direction: column;
        align-items: center;

    }
    .input-wrapper {
        display: flex;
        flex-direction: column;
        width: 50%;
        height: 100%;
        align-items: center;
        justify-content: center;
        margin-top: 30px;
    }

    .focus {
        margin-top: -7px;
        font-size: 0.8em;
    }

    form {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
    }


    label {
        height: 50px;
        margin-bottom: 20px;
    }

    input {
        background: transparent;
        border: 0;
        border-bottom: 2px solid var(--cyan);
        color: var(--text-cyan-p);
        width: 100%;
    }

    input ~ span {
        position: absolute;
        transition: all .5s ease;
        margin-top: 10px;
        color: var(--text-cyan-p)
    }

    label {
        display: flex;
        position: relative;
    }

    button {
        width: 40%;
        min-width: 170px;
        padding: 15px;
        border: 1px solid var(--blue);
        color: var(--blue);
        border-radius: 50px;

    }

    button:hover {
        background: var(--most-dark-color);
    }

    button:active {
        background: var(--most-dark-color);
        border-color: var(--text-blue-span);
        color: var(--text-blue-span);

    }

    button:focus {
        background: var(--most-dark-color);
        border-color: var(--text-blue-span);
        color: var(--text-blue-span);
    }

    .title {
        font-size: 3em;
        font-weight: 500;
        padding: 0;
        margin: 0;
        color: var(--text-cyan);
    }
</style>