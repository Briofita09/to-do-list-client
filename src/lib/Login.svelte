<script>
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
    function handleSubmit(e){
        e.preventDefault()
        console.log(name, email, password, question, answer)
        let user = {name, email, password, question, answer}
        axios.post('http://localhost:4000/sign-up', user)
        name = ''
        email = ''
        password = ''
        question = ''
        answer = ''
    }
</script>

<main>

    <h1>Faça seu cadastro</h1>

    <form>
        <label for='name'>Nome:</label>
        <input type='text' id='name' name='name' bind:value={name}/>
        <label for='email'>E-mail:</label>
        <input type='text' id='email' name='email' bind:value={email}/>
        <label for='password'>Senha:</label>
        <input type='text' id='password' name='password' bind:value={password}/>
        <label for='question'>Question:</label>
        <select id='question' for='question' name='question' bind:value={question}>
            <option>{questions[0]}</option>
            <option>{questions[1]}</option>
            <option>{questions[2]}</option>
            <option>{questions[3]}</option>
            <option>{questions[4]}</option>
        </select>
        <label for='answer'>Resposta:</label>
        <input type='text' id='answer' name='answer' bind:value={answer}/>
        <button type="submit" on:click={handleSubmit}>Cadastrar!</button>
    </form>



</main>