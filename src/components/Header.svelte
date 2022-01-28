<script>
  import { useLocation, Link } from "svelte-navigator";
  import Icon from "./Icon.svelte";

  const location = useLocation();
  let width;

  $: currentPath = $location.pathname;
</script>

<svelte:window bind:innerWidth={width} />

<header>
  <div class="container">
    <h1 class="logo"><Link to="/">🎲 Randomizer</Link></h1>
    <nav>
      {#if currentPath !== "/" && width > 640}
        <Link to="/" class="btn"
          ><Icon name="home" color="orangered" /> Inicio</Link
        >
      {/if}
      <a href="https://programadorweb.dev" class="btn" target="_blank"
        ><Icon name="comment-dots" color="orangered" /> Contacta</a
      >
    </nav>
  </div>
</header>

<style>
  header {
    position: sticky;
    padding: 10px 0px;
    background-color: #1b1b1b;
  }

  header .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  .logo {
    font-family: "Roboto", sans-serif;
    font-weight: 700;
  }

  .logo > :global(a) {
    color: #fff;
    text-decoration: none;
  }

  nav {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-end;
  }

  @media (max-width: 641px) {
    h1 {
      font-size: 22px;
    }
  }
</style>
