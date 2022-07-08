<script>
    import axios from 'axios'
    import {onMount} from 'svelte'

    import {secretToken} from '../stores/stores.js'

    let expanded = null;
    let done = false;
    let token;
    secretToken.subscribe(value => {
        token = value
    })
    
    let config = {
        headers: { Authorization: `Bearer ${token}` }
    }
    let cards = [];
    onMount( async ()=> {
        const res = await axios.get('http://localhost:4000/get-all', config)
        // @ts-ignore
        cards = await res.data
    } )

    function showText(id){
        expanded = expanded === id ? null : id
    }   

</script>
<main>
    <h1>Lista de afazeres</h1>

<div class="to-do-list">
    {#each cards as card }
        <div class="card">
            <div class="card-header" class:done>
                <h1 on:click = {showText(card.id)}>{card.title}</h1>
                <input type="checkbox" checked={card.isDone}>
            </div>
            {#if card.id === expanded}
            <h3 class='dropdown' class:expanded>{card.text}</h3> 
            {:else}
            <h3 class='dropdown'>{card.text}</h3>                        
            {/if}
        </div>
    {/each} 
</div>
</main>

<style>
    .dropdown.expanded{
        opacity: 1;
        visibility: visible;
    }

    .dropdown {
        opacity: 0;
        visibility: hidden;
    }

    .card{       
        width: 20em;

        border: 1px solid black;

        margin-bottom: 1em;

        word-break: break-all;
    }

    .card-header{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

</style>
