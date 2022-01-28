<script>
  import { Router, Link, Route } from "svelte-navigator";
  import { Header, Footer, Icon } from "./components";
  import { RollDice, RandomNumber, Raffle, RandomGroups } from "./pages";
</script>

<Router basepath="/randomizer">
  <Header />
  <main class="container">
    <Route path="/">
      <p>
        ¡Bienvenid@ a Randomizer! Selecciona la herramienta que deseas utilizar:
      </p>
      <div class="tools">
        <Link to="roll-dice" class="btn btn-default btn-full"
          ><Icon name="dice" color="orangered" /> Tirar un dado</Link
        >
        <Link to="random-number" class="btn btn-default btn-full"
          ><Icon name="random" color="orangered" /> Generar número aleatorio</Link
        >
        <Link to="raffle" class="btn btn-default btn-full"
          ><Icon name="trophy" color="orangered" /> Realizar sorteo</Link
        >
        <Link to="random-groups" class="btn btn-default btn-full"
          ><Icon name="users" color="orangered" /> Generar grupos aleatorios</Link
        >
      </div>
    </Route>
    <Route path="roll-dice">
      <RollDice />
    </Route>
    <Route path="random-number">
      <RandomNumber />
    </Route>
    <Route path="raffle">
      <Raffle />
    </Route>
    <Route path="random-groups">
      <RandomGroups />
    </Route>
  </main>
  <Footer />
</Router>

<style>
  main {
    padding: 25px 0px;
  }

  main p {
    margin-bottom: 25px;
  }

  .tools {
    display: flex;
    flex-direction: column;
    gap: 25px;
    font-size: 18px;
  }
</style>
