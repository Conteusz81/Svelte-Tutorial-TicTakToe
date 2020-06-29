<script>
    import Space from './componnets/Space.svelte'
    import gameStore from './stores/game-store.js'

    let board = ["", "", "", "", "", "", "", "", ""];
    let nextPlayer = "";
    let winner = "";
    let numberOfPeople = 0;

    gameStore.subscribe(data => {
        console.log(data);
        if (!data) { return; }

       winner = data.winner;
       nextPlayer = data.nextPlayer;
       board = data.board;
       numberOfPeople = data.numberOfPeeps;
    });
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
        <Space space={board[0]} />
        <Space space={board[1]} />
        <Space space={board[2]} />
        <Space space={board[3]} />
        <Space space={board[4]} />
        <Space space={board[5]} />
        <Space space={board[6]} />
        <Space space={board[7]} />
        <Space space={board[8]} />
    </div>
    {#if winner}
    <button>New Game</button>
    {/if}
</main>

