<script>

    import Cinema from './Cinema.svelte'
    import DateList from './DateList.svelte'
    import {getContext} from 'svelte'
    import {fly} from 'svelte/transition'

    const {title} = getContext('film_info')

    function printForm() {
        console.log('Телефон:', phoneInput);
        console.log('ФИО:', nameInput);
    }

    let phoneInput = '';//
    let nameInput = '';

    let smallerPhone = phoneInput !== '';
    let smallerName = nameInput !== '';

    let chosenDate = undefined;
    let chosenSeats = [];
    let animationPlay = false;

    function phoneValidation() {
        let last = phoneInput.length-1
        if (phoneInput === '+'){
            return;
        }
        if ('0123456789'.includes(phoneInput[last])){
            if (phoneInput[0] === '8'){
                phoneInput = '+7' + phoneInput.slice(1, last);
            }

            if (phoneInput.length === 3){
                phoneInput = phoneInput.slice(0, 2) + '(' + phoneInput[2];
            }
            if (phoneInput.length === 7){
                phoneInput = phoneInput.slice(0, 6) + ')' + phoneInput[6];
            }
            if (phoneInput.length === 7){
                phoneInput = phoneInput.slice(0, 6) + ')' + phoneInput[6];
            }
            if (phoneInput.length === 11){
                phoneInput = phoneInput.slice(0, 10) + '-' + phoneInput[10];
            }
            if (phoneInput.length === 14){
                phoneInput = phoneInput.slice(0, 13) + '-' + phoneInput[13];
            }
            if (phoneInput.length > 16){
                phoneInput = phoneInput.slice(0, 16)
            }
        }
        else {
            phoneInput = phoneInput.slice(0, last)
        }
    }
</script>


<div class="component">
    <h1 class="title">{title}</h1>
    <form>
        <div class="input-wrapper">

            <label><input bind:value={phoneInput} type="phone"
                          on:focus={() => smallerPhone = true}
                          on:blur={() => smallerPhone = phoneInput !== ''}
                          on:input={phoneValidation}>
                <span class:focus={smallerPhone}>Телефон</span></label>

            <label><input bind:value={nameInput} type="name"
                          on:focus={() => smallerName = true}
                          on:blur={() => smallerName = nameInput !== ''}>
                <span class:focus={smallerName}>ФИО</span></label>
            <button class="submit" type="button" on:click={printForm}>Забронировать</button>
        </div>
        <div class="animation-wrapper">
            {#if chosenDate !== undefined}
                <div class="cinema-wrapper" transition:fly={{'x': 50}}>
                    <button class="back-button" type="button" on:click={() => chosenDate = undefined}>&#8592 Назад</button>
                    <Cinema/>
                </div>
            {:else}
                <div class="date-wrapper" transition:fly={{x: -50}}>
                    <DateList bind:chosen={chosenDate}/>
                </div>
            {/if}
        </div>


    </form>
</div>

<style>
    @media all and (max-width: 700px) {
        form {
            flex-direction: column-reverse;
            margin-left: 32px;
        }
        .animation-wrapper {
            width: 70%;
        }
        .cinema-wrapper {
            margin: 40px 0;
            align-items: center;
        }
        .title {
            margin-bottom: 15px;
        }
    }
    @media all and (min-width: 700px) {
        form {
            flex-direction: row;
        }
        .animation-wrapper {
            width: 50%;
        }
        .title {
            margin: 0;
        }
    }
    .component {
        margin-left: 5px;
        display: flex;
        width: 100%;
        height: 90%;
        flex-direction: column;
        align-items: center;

    }
    .back-button {
        border: none;
        padding: 5px;
        width: 100px;
        color: var(--text-blue-span);
        cursor: pointer;
    }
    .back-button:active {
        background: transparent;
    }

    .date-wrapper {
        position: absolute;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .animation-wrapper {
        position: relative;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .cinema-wrapper {
        position: absolute;
        display: flex;
        justify-content: center;

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

    .cinema-wrapper {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;

    }

    .focus {
        margin-top: -7px;
        font-size: 0.8em;
    }

    form {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        text-align: center;
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

    .submit {
        width: 40%;
        min-width: 170px;
        padding: 15px;
        border: 1px solid var(--blue);
        color: var(--blue);
        border-radius: 50px;

    }

    .submit:hover {
        background: var(--most-dark-color);
    }

    .submit:active, .submit:focus {
        background: var(--most-dark-color);
        border-color: var(--text-blue-span);
        color: var(--text-blue-span);

    }

    .title {
        font-size: 3em;
        font-weight: 500;
        padding: 0;
        color: var(--text-cyan);
    }
</style>