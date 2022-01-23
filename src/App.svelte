<script>
  import { Router, Link, Route } from "svelte-navigator";
  import { Header, Footer } from "./components";
  import { RollDice, RandomNumber, Raffle } from "./pages";

  const getRoute = path => {
    return `${process.env.isProd ? `${BASE_PATH}/` : ""}${path}`;
  };
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
          >🎲 Tirar un dado</Link
        >
        <Link to="random-number" class="btn btn-default btn-full"
          >🔀 Generar número aleatorio</Link
        >
        <Link to="raffle" class="btn btn-default btn-full"
          >🏆 Realizar sorteo</Link
        >
        <Link to="/" class="btn btn-default btn-full btn-disabled"
          >👪 Generar grupos aleatorios (en desarrollo)</Link
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
