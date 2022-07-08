<script>
    import axios from "axios"
    import {useNavigate, link} from "svelte-navigator"
    import {secretToken} from "../stores/stores.js"

    let email= ''
    let password =''
    const navigate = useNavigate()

    async function handleSubmit(e){
        try{
            e.preventDefault()
            let user ={email, password}
           const response = await axios.post('http://localhost:4000/login', user)
           if(response.status === 200){
               secretToken.update(value => {return value = response.data.token})
               navigate('/cards')
           }
        } catch(err){
            alert(err)
        }       
    }

</script>

<main>

    <h1>Faça Login!</h1>

    <form>
        <div>
            <label for='email'>E-mail:</label>
            <input type='text' id='email' name='email' bind:value={email}/>
        </div>
        <div>
            <label for='password'>Senha:</label>
            <input type='text' id='password' name='password' bind:value={password}/>
        </div>
        <button type="submit" on:click={handleSubmit}>Login!</button>
    </form>
    <a href='/' class="my-link" use:link><h3>Não é cadastrado, faça seu cadastro aqui!</h3></a>
</main>

<style>
h1, h3{
    text-align: center;
    
}

.my-link {
    color: black;
    text-decoration: none;
}
form {
    display: flex;
    flex-direction: column;
    align-items: center;

    margin: 0 10%;

    border: 1px solid black;
}

label {
    text-align: start;
}

form input{
    margin: 10px 0;
    width: 150px;
}

button{
    width: 70px;
    height: 40px;
    margin-bottom: 10px;
}
</style>