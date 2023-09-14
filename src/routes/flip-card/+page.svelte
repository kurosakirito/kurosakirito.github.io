<svelte:head>
	<title>Flip Card</title>
	<meta name="description" content="Flip Card Game" />
</svelte:head>

<script>
    import ImageTile from './ImageTile.svelte';
    import cinnamoroll from '$lib/images/cinnamoroll.png';
    import pompompurin from '$lib/images/pompompurin.png';
    import pochacco from '$lib/images/pochacco.png';
    import kuromi from '$lib/images/kuromi.png';
    import ahirunopekkle from '$lib/images/ahirunopekkle.png';
    import badbadtzmaru from '$lib/images/badbadtzmaru.png';
    import cogimyun from '$lib/images/cogimyun.png';
    import kerokerokeroppi from '$lib/images/kerokerokeroppi.png';
    import littletwinstars from '$lib/images/littletwinstars.png';
    import minnanotabo from '$lib/images/minnanotabo.png';
    import tuxedosam from '$lib/images/tuxedosam.png';

    let flipCount = 0;

    function shuffle(array) {
        let currentIndex = array.length, randomIndex;
        while (currentIndex != 0) {
            randomIndex = Math.floor(Math.random() * currentIndex);
            currentIndex--;
            [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
        }
        return array;
    }

    let characters = [];
    characters = [ ...characters, {id: 1, name: cinnamoroll, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 2, name: cinnamoroll, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 3, name: pompompurin, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 4, name: pompompurin, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 5, name: pochacco, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 6, name: pochacco, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 7, name: kuromi, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 8, name: kuromi, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 9, name: ahirunopekkle, flipped: false, completed: false} ];
    characters = [ ...characters, {id: 10, name: ahirunopekkle, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 11, name: badbadtzmaru, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 12, name: badbadtzmaru, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 13, name: cogimyun, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 14, name: cogimyun, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 15, name: kerokerokeroppi, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 16, name: kerokerokeroppi, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 17, name: littletwinstars, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 18, name: littletwinstars, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 19, name: minnanotabo, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 20, name: minnanotabo, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 21, name: tuxedosam, flipped: false, completed: false} ];
//    characters = [ ...characters, {id: 22, name: tuxedosam, flipped: false, completed: false} ];
    shuffle(characters);
    
    const checkComplete = (c) => {
        if (c.completed) {
            return;
        }
        flipCount ++;
        characters.forEach(char => {
            if (char.id == c.id) {
                char.flipped = true;
            }
        });
        characters = characters;
        const flippedCharacters = characters.filter((char) => char.flipped == true);
        for (let idx in flippedCharacters) {
            if (flippedCharacters[idx].id != c.id && flippedCharacters[idx].name == c.name) {
                characters.forEach(char => {
                    if (char.name == c.name) {
                        char.completed = true;
                    }
                });
            }
        }
        if (flipCount == 2) {
            setTimeout(() => {
                characters.forEach(char => {
                    if (char.flipped && !char.completed) {
                        char.flipped = false;
                    }
                });
                characters = characters;
            }, 500);
            flipCount = 0;
        }
    }

    
</script>

<style>
    .flip-card {
        background-color: transparent;
        width: 200px;
        height: 200px;
        perspective: 1000px;
    }
    
    .flip-card-inner {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: center;
        transition: transform 0.6s;
        transform-style: preserve-3d;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2)
    }
    
    .flip-card:hover .flip-card-inner {
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
/*        color: black;*/
    }
    
    .flip-card-back {
/*        background-color: blue;*/
/*        color: white;*/
        transform: rotateY(180deg);
    }
    
    .row {
/*        display: grid;*/
/*        grid-column: auto;*/
    }
    
    .card-group {
/*        display: flex;*/
/*        flex-direction: row;*/
/*        flex-wrap: wrap;*/
        display: grid;
        grid-template-columns: 300px 300px 300px 300px 300px;
        justify-content: center;
    }
/*    .card-group>* {*/
/*        flex: 1 1 80px;*/
/*    }*/
</style>

<h1>Flip Card</h1>

<div class="card-group">
    {#each characters as character, i}
        <ImageTile bind:character
            on:flip={(e) => checkComplete(e.detail)}/>
    {/each}
</div>