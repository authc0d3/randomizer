<script>
  import { Router, Link, Route } from "svelte-navigator";
  import Fa from "svelte-fa";
  import {
    faDice,
    faRandom,
    faTrophy,
    faUsers
  } from "@fortawesome/free-solid-svg-icons";
  import { Header, Footer } from "./components";
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
          ><Fa icon={faDice} color="orangered" /> Tirar un dado</Link
        >
        <Link to="random-number" class="btn btn-default btn-full"
          ><Fa icon={faRandom} color="orangered" /> Generar número aleatorio</Link
        >
        <Link to="raffle" class="btn btn-default btn-full"
          ><Fa icon={faTrophy} color="orangered" /> Realizar sorteo</Link
        >
        <Link to="random-groups" class="btn btn-default btn-full"
          ><Fa icon={faUsers} color="orangered" /> Generar grupos aleatorios</Link
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
