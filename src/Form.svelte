<script>
    function printForm() {
        console.log('Телефон:', phoneInput);
        console.log('ФИО:', nameInput);
    }

    let phoneInput = '';
    let nameInput = '';

    let smallerPhone = phoneInput !== '';
    let smallerName = nameInput !== '';


</script>


<form>
    <label><input bind:value={phoneInput} type="phone"
                  on:focus={() => smallerPhone = true}
                  on:blur={() => smallerPhone = phoneInput !== ''}>
        <span class:focus={smallerPhone}>Телефон</span></label>

    <label><input bind:value={nameInput} type="name"
                  on:focus={() => smallerName = true}
                  on:blur={() => smallerName = nameInput !== ''}>
        <span class:focus={smallerName}>ФИО</span></label>

    <button type="button" on:click={printForm}>Забронировать</button>
</form>


<style>
    .focus {
        margin-top: -7px;
        font-size: 0.8em;
    }

    form {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        height: 90%;
        width: 100%;
    }

    label {
        height: 50px;
        margin-top: 10px;
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
        padding: 15px;
        border: 1px solid var(--blue);
        color: var(--blue);
        border-radius: 50px;

    }

    button:hover{
        background: var(--most-dark-color);
    }
    button:active{
        background: var(--most-dark-color);
        border-color: var(--text-blue-span);
        color: var(--text-blue-span);

    }
    button:focus{
        background: var(--most-dark-color);
        border-color: var(--text-blue-span);
        color: var(--text-blue-span);
    }

</style>