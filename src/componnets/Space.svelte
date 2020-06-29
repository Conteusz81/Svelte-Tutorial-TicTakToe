<script>
    export let space = "";
    export let winner;
    $: won = space === winner;
</script>

<style>
    .space {
        border: 1px solid #666565;
        height: 125px;
        width: auto;
        font-size: 75px;
        text-align: center;
        line-height: 125px;
        cursor: pointer;
    }
    .winning {
        color: purple;
    }
</style>

<div class="space" on:click class:winning={won}>
    {space}
</div>
