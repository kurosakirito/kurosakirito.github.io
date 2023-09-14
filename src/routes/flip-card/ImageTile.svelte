<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    export let character = 'inner';

    let active = 0;
    let turn = 0;

    export let characters;
    let completed = true;
    let flipped = false;
    const flip = (c) => {
        dispatch("flip", c);
    }

</script>

<style>
    .flip-card {
        background-color: transparent;
        width: 300px;
        height: 300px;
        perspective: 1000px;
    }

    .flip-card-inner {
        position: relative;
        width: 200px;
        height: 200px;
/*        width: 100%;*/
/*        height: 100%;*/
        text-align: center;
        transition: transform 0.6s;
        transform-style: preserve-3d;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2)
    }

/*    .flip-card:hover .flip-card-inner {*/
/*        transform: rotateY(180deg);*/
/*    }*/
    
    .flip-card-inner-active {
        transform: rotateY(180deg);
    }

    .flip-card-front, .flip-card-back {
        position: absolute;
        width: 100%;
        height: 100%;
        -webkit-backface-visibility: hidden;
        backface-visibility: hidden;
    }

    .flip-card-front {
        background-color: #bbb;
    }

    .flip-card-back {
        transform: rotateY(180deg);
    }
</style>

<div class="flip-card" style="margin: 50px;">
    <div class="flip-card-inner" on:click={flip(character)} class:flip-card-inner-active={character.flipped}>
        <div class="flip-card-front">

        </div>
        <div class="flip-card-back">
            <img style="width: 200px; height: 200px;" src="{character.name}" alt="Avatar" />
        </div>
    </div>
</div>