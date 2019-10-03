<template>
    <div>
        <div id="board" class="bg-gray-900">
            <div class="grid-area bg-white">
                <p>What went well?</p>
            </div>
            <div class="grid-area bg-white">
                <p>What went wrong?</p>
            </div>
            <div class="grid-area bg-white">
                <p>What We Should Start Doing</p>
            </div>
            <div class="grid-area bg-white">
                <p>What We Should Stop Doing</p>
            </div>
        </div>
        <slot></slot>
    </div>
</template>

<script>
export default {

}
</script>

<style>
    #board {
        display: grid;
        grid-template-rows: 1fr 1fr;
        grid-template-columns: 1fr 1fr;
        grid-gap: 10px;
        width: 100%;
        height: 100%;
        position: absolute;
        overflow: hidden;
    }

    .grid-area p {
        text-align: center;
        margin-top: 2rem;
        pointer-events: none;
        z-index: 10000;
        position: relative;
    }
</style>