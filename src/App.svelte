<script>
    import Space from './componnets/Space.svelte'
    import gameStore from './stores/game-store.js'

    gameStore.subscribe(data => {
        console.log(data, 'data from store');
    })
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
    <h2>Number of people playing:</h2>
    <h2>Player X</h2>

    <div class="game-board">
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
        <Space space="X" />
    </div>
    <button>New Game</button>
</main>

