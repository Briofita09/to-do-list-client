<script>
    import {link} from "svelte-navigator"
    import axios from 'axios'

    let questions = [
        'Qual o nome da sua mãe?',
        'Qual o nome do seu pet?',
        'Qual a sua cor favorita?',
        'Qual a sua comida favorita?',
        'Qual o seu esporte favorito?'
    ]
    let name = ''
    let email = ''
    let password = ''
    let question = ''
    let answer = ''
    async function handleSubmit(e){
        try{
            e.preventDefault()
        console.log(name, email, password, question, answer)
        let user = {name, email, password, question, answer}
       await axios.post('http://localhost:4000/sign-up', user)
        name = ''
        email = ''
        password = ''
        question = ''
        answer = ''
        } catch(err){
            alert(err.response.statusText)
        }
    }
</script>

<main>

    <h1>Faça seu cadastro</h1>

    <form>
        <div>
            <label for='name'>Nome:</label>
            <input type='text' id='name' name='name' bind:value={name}/>
        </div>
        <div>
            <label for='email'>E-mail:</label>
            <input type='text' id='email' name='email' bind:value={email}/>
        </div>
        <div>
            <label for='password'>Senha:</label>
            <input type='text' id='password' name='password' bind:value={password}/>
        </div>
        <div>
            <label for='question'>Question:</label>
            <select id='question' for='question' name='question' bind:value={question}>
                {#each questions as question }
                <option>{question}</option>                    
                {/each}
            </select>
        </div>
        <div>
            <label for='answer'>Resposta:</label>
            <input type='text' id='answer' name='answer' bind:value={answer}/>
        </div>
        <button type="submit" on:click={handleSubmit}>Cadastrar!</button>
    </form>

    <a href="/login" class='my-link' use:link><h3 class="login-link">Já possui cadastro? Faça login</h3></a>
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

form input, form select{
    margin: 10px 0;
    width: 150px;
}

button{
    width: 100px;
    height: 50px;
    margin-bottom: 10px;
}
</style>