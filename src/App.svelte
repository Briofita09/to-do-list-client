<script>
import {Router, Route} from "svelte-navigator"
import Cards from "./lib/Cards.svelte"
import Login from "./lib/Login.svelte"
import SignUp from './lib/SignUp.svelte'
</script>

<main>
  <Router>
    <Route path='/'><SignUp/></Route>
    <Route path='/login'><Login/></Route>
    <Route path='/cards'><Cards/></Route>
  </Router>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
</style>
