<script>
    import Space from './componnets/Space.svelte'
    import gameStore from './stores/game-store.js'
    import { nextMove, reset } from './requests.js';

    let board = ["", "", "", "", "", "", "", "", ""];
    let nextPlayer = "";
    let winner = "";
    let numberOfPeople = 0;
    let errorMessage;

    gameStore.subscribe(data => {
        console.log(data);
        if (!data) { return; }

       winner = data.winner;
       nextPlayer = data.nextPlayer;
       board = data.board;
       numberOfPeople = data.numberOfPeeps;
    });

    async function takeSpace(space) {
        if (winner || !gameStore.isConnected) { return; }

        errorMessage = await nextMove(space);
    }

    async function newGame() {
        errorMessage = await reset();
    }
</script>

<style>
    main {
        width: 475px;
        margin: 0 auto;
    }

    .game-board {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(3, 1fr);
    }

    button {
        width: 100%;
        margin-top: 20px;
        padding: 10px 0;
        border: none;
        border-radius: 0;
        background-color: lightblue;
        font-size: 30px;
        cursor: pointer;
    }
    button:hover {
        outline: none;
    }

    .error-message {
        color: red;
        font-size: 20px;
    }

</style>

<main>
    <h1>Tic Tak Toe</h1>
    <h2>Number of people playing: {numberOfPeople}</h2>
    {#if winner ==='TIE'}
    <h2>Tie Game!!!</h2>
    {:else if winner}
    <h2>Player {winner} won!!!</h2>
    {:else}
    <h2>Player {nextPlayer}</h2>
    {/if}
    <div class="game-board">
        <Space {winner} space={board[0]} on:click={() => takeSpace(0)} />
        <Space {winner} space={board[1]} on:click={() => takeSpace(1)} />
        <Space {winner} space={board[2]} on:click={() => takeSpace(2)} />
        <Space {winner} space={board[3]} on:click={() => takeSpace(3)} />
        <Space {winner} space={board[4]} on:click={() => takeSpace(4)} />
        <Space {winner} space={board[5]} on:click={() => takeSpace(5)} />
        <Space {winner} space={board[6]} on:click={() => takeSpace(6)} />
        <Space {winner} space={board[7]} on:click={() => takeSpace(7)} />
        <Space {winner} space={board[8]} on:click={() => takeSpace(8)} />
    </div>
    {#if winner}
    <button on:click={newGame}>New Game</button>
    {/if}
    {#if errorMessage}
        <p class="error-message">{errorMessage}</p>
    {/if}
</main>

