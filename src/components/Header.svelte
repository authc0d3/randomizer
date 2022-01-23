<script>
  import { useLocation, Link } from "svelte-navigator";

  const location = useLocation();
  let width;

  $: currentPath = $location.pathname;
</script>

<svelte:window bind:innerWidth={width} />

<header>
  <div class="container">
    <h1 class="logo"><Link to="/randomizer">🎲 Randomizer</Link></h1>
    <nav>
      {#if currentPath !== "randomizer" && width > 640}
        <Link to="/randomizer" class="btn">🏠 Inicio</Link>
      {/if}
      <a href="https://programadorweb.dev" class="btn" target="_blank"
        >💬 Contacta</a
      >
    </nav>
  </div>
</header>

<style>
  header {
    position: sticky;
    padding: 10px 0px;
    background-color: rgb(33, 51, 51);
  }

  header .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  .logo {
    font-family: "Mochiy Pop P One", sans-serif;
    font-weight: normal;
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
