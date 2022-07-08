<script>
    import axios from 'axios'
    import {onMount} from 'svelte'

    import {secretToken} from '../stores/stores.js'


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
</script>
<h1>Lista de afazeres</h1>

<div class="to-do-list">
    {#each cards as card }
        <h1>{card.title}</h1>
        <h3>{card.text}</h3>
    {/each}
</div>